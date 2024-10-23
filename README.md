# Minificação de Arquivos do Projeto

Este projeto utiliza ferramentas para minificar arquivos HTML, JavaScript e CSS, a fim de melhorar o desempenho e dificultar o acesso ao código-fonte legível. Este tutorial irá guiá-lo desde a inicialização do `npm` no projeto até a minificação dos arquivos.

## Passos para Configuração

### 1. Inicializando o `npm`

Se o `npm` ainda não estiver inicializado no projeto, siga estes passos:

1. Abra o terminal na pasta do projeto.
2. Execute o comando abaixo para criar o arquivo `package.json`, que gerenciará as dependências do projeto:
   ```bash
   npm init -y
   ```

npm install html-minifier-terser terser clean-css-cli --save-dev

"scripts": {
"minify:html": "html-minifier-terser --collapse-whitespace --remove-comments --minify-css true --minify-js true -o index.min.html index.html && html-minifier-terser --collapse-whitespace --remove-comments --minify-css true --minify-js true -o results.min.html results.html",
"minify:js": "terser script.js -o script.min.js",
"minify:css": "cleancss -o style.min.css style.css",
"minify:all": "npm run minify:html && npm run minify:js && npm run minify:css"
}

npm run minify:html
npm run minify:js
npm run minify:css
npm run minify:all
