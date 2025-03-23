
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
   O projeto será executado em `http://localhost:3000`

4. **Para construir para produção**
   ```bash
   npm run build
   ```
   
   Os arquivos de produção serão gerados na pasta `dist`

5. **Para executar a versão de produção localmente**
   ```bash
   npm run preview
   ```

## Configuração do servidor em produção

Para implantar em um servidor de produção, você deve:

1. Executar `npm run build` para gerar os arquivos otimizados
2. Copiar todo o conteúdo da pasta `dist` para a pasta raiz do seu servidor web
3. Configurar o servidor para redirecionar todas as requisições para o arquivo `index.html` (necessário para o React Router funcionar)

### Exemplo de configuração para Nginx:
```nginx
server {
    listen 80;
    server_name seu-dominio.com;
    root /caminho/para/pasta/dist;
    
    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

### Exemplo de configuração com arquivo .htaccess para Apache:
```apache
<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /index.html [L]
</IfModule>
```

## Tecnologias utilizadas
- Vite
- TypeScript
- React
- React Router
- shadcn-ui
- Tailwind CSS
- Framer Motion
