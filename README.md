
# Projeto FGTS

## Como executar o projeto localmente

Para executar este projeto em seu ambiente local, siga estas etapas:

1. **Clone o repositório**
   ```bash
   git clone https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git
   cd SEU-REPOSITORIO
   ```

2. **Instale as dependências**
   ```bash
   npm install
   ```

3. **Execute o servidor de desenvolvimento**
   ```bash
   npm run dev
   ```
   O projeto será executado em `http://localhost:8080`

4. **Para construir para produção**
   ```bash
   npm run build
   ```
   
   Os arquivos de produção serão gerados na pasta `dist`

5. **Para executar a versão de produção localmente**
   ```bash
   npm run preview
   ```

## Configuração em servidor VPS (produção)

### Pré-requisitos
- Node.js (versão 16 ou superior)
- NPM
- Servidor web (Apache ou Nginx)

### Passos para instalação em VPS

1. **Conecte-se à sua VPS via SSH**
   ```bash
   ssh usuario@seu-servidor
   ```

2. **Clone o repositório**
   ```bash
   git clone https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git
   cd SEU-REPOSITORIO
   ```

3. **Instale as dependências e construa o projeto**
   ```bash
   npm install
   npm run build
   ```

4. **Configure o servidor web**

   #### Para Apache:
   
   1. Copie os arquivos da pasta `dist` para a pasta do servidor web:
      ```bash
      sudo cp -r dist/* /var/www/html/
      ```
      
   2. Ative os módulos necessários:
      ```bash
      sudo a2enmod rewrite
      sudo a2enmod mime
      sudo a2enmod expires
      sudo a2enmod deflate
      ```
      
   3. Certifique-se de que o arquivo `.htaccess` esteja na raiz do site e tenha as permissões corretas:
      ```bash
      sudo chmod 644 /var/www/html/.htaccess
      ```
      
   4. Configure o VirtualHost para permitir o uso do .htaccess:
      ```bash
      sudo nano /etc/apache2/sites-available/000-default.conf
      ```
      
      Adicione estas linhas dentro da seção `<VirtualHost>`:
      ```apache
      <Directory /var/www/html>
          AllowOverride All
          Require all granted
      </Directory>
      ```
      
   5. Reinicie o Apache:
      ```bash
      sudo systemctl restart apache2
      ```

   #### Para Nginx:
   
   1. Copie os arquivos da pasta `dist` para a pasta do servidor web:
      ```bash
      sudo cp -r dist/* /var/www/html/
      ```
      
   2. Crie ou edite a configuração do site:
      ```bash
      sudo nano /etc/nginx/sites-available/default
      ```
      
   3. Use a configuração do arquivo `nginx.conf` fornecido no projeto
   
   4. Verifique a configuração e reinicie o Nginx:
      ```bash
      sudo nginx -t
      sudo systemctl restart nginx
      ```

5. **Configure o servidor backend (se necessário)**
   ```bash
   # Instale o PM2 para gerenciar o processo Node.js
   npm install -g pm2
   
   # Inicie o servidor backend
   pm2 start server.js
   
   # Configure o PM2 para iniciar na inicialização do sistema
   pm2 startup
   pm2 save
   ```

### Solução para problemas comuns

#### Problema de MIME Type para arquivos JavaScript
Se você encontrar erros de MIME type no console, como:
```
Refused to execute script because its MIME type ('application/octet-stream') is not executable.
```

**Para Apache:**
- Verifique se o módulo `mime` está ativado: `sudo a2enmod mime`
- Certifique-se de que o `.htaccess` contém as definições de tipo MIME corretas
- Reinicie o Apache: `sudo systemctl restart apache2`

**Para Nginx:**
- Verifique se o arquivo de configuração inclui as definições de tipo MIME corretas
- Reinicie o Nginx: `sudo systemctl restart nginx`

## Tecnologias utilizadas
- Vite
- TypeScript
- React
- React Router
- shadcn-ui
- Tailwind CSS
- Framer Motion
