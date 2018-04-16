[início](https://github.com/uxluissilva/ux-docs)

# Front-end stack tools

Documentação referente à estrutura de desenvolvimento front-end da aplicação Hospitalar Benner. 


## O que contém?
São utilizadas tecnologias para facilitar o desenvolvimento do front-end e garantir maior consistência nos códigos referentes aos componentes e estilos do sistema, essas tecnologias ajudam com a automatização de tarefas com o runner [Gulp](https://gulpjs.com/) e a criação de variáveis de estilo e otimização do CSS com o [SASS](https://sass-lang.com/).

### Tecnologias:

- [Node e NPM](https://nodejs.org/en/)
- [Ruby on Rails](https://rubyinstaller.org/)
- [SASS - pré-processador CSS](https://sass-lang.com/)
- [Gulp - Task Runner](https://gulpjs.com/)


### NPM Packages ![NPM logo](https://github.com/uxluissilva/ux-docs/blob/master/img/npm.png)

Os pacotes que são utilizados encontram-se em `Interface\Estrutura\`, são utilizados os pacotes de acordo com o `package.json` do projeto. Caso o projeto ainda não possua um arquivo `package.json`, adicionar o código abaixo na estrutura principal e instalar com `npm install`.

Exemplo abaixo da primeira versão utilizada:
```json
{
  "version": "1.0.0",
  "name": "asp.net",
  "private": true,
  "devDependencies": {
    "gulp": "v4.0.0",
    "node-sass": "^4.7.2",
    "npm": "v5.6.0"
  },
  "dependencies": {
    "browser-sync": "^2.23.6",
    "gulp-autoprefixer": "^4.1.0",
    "gulp-clean-css": "^3.9.2",
    "gulp-cli": "^2.0.1",
    "gulp-rename": "^1.2.2",
    "gulp-sass": "^3.1.0"
  }
}
```


### Gulp ![Gulp logo](https://github.com/uxluissilva/ux-docs/blob/master/img/gulp.png)

O arquivo `gulpfile.js` é responsável pelas atividades executadas pelo Gulp, essas são as tarefas configuradas que serão executadas para pré-processar os arquivos SASS e outros configurados. Caso o projeto não possua um arquivo de configuração `gulpfile.js`, deve ser adicionado o arquivo na estrutura principal do projeto e adicionado o código abaixo ou similar de configuração, para que seja possível rodar o Gulp.

É importante citar, que o Gulp está configurado para rodar na pasta `scss` com base no arquivo `main.scss`, portanto estes são essenciais para a estrutura de SASS do projeto.

Veja abaixo o exemplo do gulpfile na primeira versão:
```javascript
/*
This file is the main entry point for defining Gulp tasks and using Gulp plugins.
Click here to learn more. https://go.microsoft.com/fwlink/?LinkId=518007
*/

var gulp = require('gulp');
var sass = require('gulp-sass');
var browserSync = require('browser-sync').create();
var rename = require('gulp-rename');
var cleanCSS = require('gulp-clean-css');
var autoprefixer = require('gulp-autoprefixer');

var input = './scss/main.scss';
var inputSCSS = './scss/**/*.scss';
var output = './css';

var sassOptions = {
    errLogToConsole: true,
    outputStyle: 'expanded'
}

gulp.task('sass', function() {
    return gulp
        .src(input)
        .pipe(sass(sassOptions).on('error', sass.logError))
        .pipe(autoprefixer())
        .pipe(rename('main.css'))
        .pipe(cleanCSS({compatibility: 'ie8'}))
        .pipe(gulp.dest(output));
});

gulp.task('watch', function() {
    return gulp
        // Watch the input folder for change,
        // and run 'sass' task when something happens
        .watch(inputSCSS, gulp.series('sass'))
        // When there is a change
        // log a message in the console
        .on('change', function(event) {
            console.log('File ' + event.path + ' was ' + event.type + ', running tasks...');
        });
});

gulp.task('default', gulp.parallel('sass', 'watch'));
```

## The Grid - Framework Flexbox ![The Grid logo](https://github.com/uxluissilva/ux-docs/blob/master/img/the-grid.png)

Framework open-source desenvolvido para otimizar a aplicação do Flexbox no front-end das aplicações, utilizado no hospitalar para facilitar a aplicação de responsividade nas interfaces do sistema.

- [Referência The Grid - Flexbox](http://quinalha.me/the-grid/)
- [Repositório GitHub](https://github.com/gustavoquinalha/the-grid)




## Como instalar e configurar?
Processo de instalação e configuração da estrutura de desenvolvimento com as ferramentas para front-end, só precisa ser executado uma vez.

1. Baixe e instale a versão LTS do [NodeJS](https://nodejs.org/en/) (já inclui o NPM)
2. Baixe e instale a versão LTS do Ruby on Rails, utilize o [Ruby Installer](https://rubyinstaller.org/) para Windows
3. Abra o Prompt de Comando e verifique a versão dos programas instalados

  - NodeJS - `$ node -v`
  - NPM - `$ npm -v`
  - Ruby on Rails - `$ ruby -v`

Com o repositório do projeto [Hospitalar Aplicação](https://github.com/bennersaude/Hospitalar_Aplicacao) já clonado na máquina e selecionada a branch correta para a versão com SASS (atualmente `v14\develop`).

4. Abra o Visual Studio e faça o build do projeto Interface 
  - Necessário solucionar erros de build se houverem
5. Abra o **Package Manager Console** e navegue até a pasta `Interface\Estrutura\`
  - Com o console aberto verifique o diretório digitando - `$ pwd`
  - Navegue até a pasta Estrutura - `$ cd Estrutura\`
  - Verifique a pasta atual - `$ pwd`

![Abrir Package Manager Console](https://github.com/uxluissilva/ux-docs/blob/master/img/open-pmc.png)
![Navegar até a pasta Estrutura e rodar pwd](https://github.com/uxluissilva/ux-docs/blob/master/img/pwd-console.png)

6. Ainda no **Package Manager Console**, na pasta Estrutura, instale as dependências do projeto
  - Instale as dependências com o NPM - `$ npm i`

7. Para garantir as referências no projeto, utilize o exporer e abra a pasta da Estrutura
  - Clique com botão direto no `gulpfile.js`
  - Selecione a opção "Configure External Tools"
  - Mova o `$PATH` para a primeira linha, conforme imagem abaixo

![No file explorer, entrar na pasta estrutura e clicar c/ botão direito no gulpfile](https://github.com/uxluissilva/ux-docs/blob/master/img/open-cet.png)

![Em Configure External Tools, imagem da GUI com $PATH em primeiro](https://github.com/uxluissilva/ux-docs/blob/master/img/garantir-refs.png)

8. Reinstalar o pacote node-sass
  - Abra o **Package Manager Console** e navegue até `$ cd Interface\Estrutura\` ou verifique  com `$ pwd`
  - Reinstale o pacote node-sass `npm i node-sass`

Pronto, todas as dependências foram instaladas, parabéns! Veja como utilizar a seguir.


## Como utilizar?
Após a instalação e configuração abra o Gerenciador do Task Runner no Visual Studio e inicie o Gulp.
- Abra o diretório `Interface\Estrutura\` no explorer do Visual Studio 

![File explorer projeto Interface](https://github.com/uxluissilva/ux-docs/blob/master/img/explorer.png)

- Clique com o botão direito no arquivo `gulpfile.js` e abrar o Task Runner Explorer

![Menu botão direito no gulpfile](https://github.com/uxluissilva/ux-docs/blob/master/img/task-runner.png)

- Inicie a task `default` no Gerenciador do Task Runner

![Iniciando a task default no gerenciador do task runner](https://github.com/uxluissilva/ux-docs/blob/master/img/gulp-default.png)
