# Documentação de Design

Documentação referente à estrutura de desenvolvimento front-end da aplicação Hospitalar Benner. 


## O que contém?
São utilizadas tecnologias para facilitar o desenvolvimento do front-end e garantir maior consistência nos códigos referentes aos componentes e estilos do sistema, essas tecnologias ajudam com a automatização de tarefas com o runner [Gulp](https://gulpjs.com/) e a criação de variáveis de estilo e otimização do CSS com o [SASS](https://sass-lang.com/).

### Tecnologias:

- [Node e NPM](https://nodejs.org/en/)
- [Ruby on Rails](https://rubyinstaller.org/)
- [SASS - pré-processador CSS](https://sass-lang.com/)
- [Gulp - Task Runner](https://gulpjs.com/)


### NPM Packages
Os pacotes que são utilizados encontram-se em `Interface\Estrutura\`, são utilizados os pacotes de acordo com o `package.json` do projeto. Exemplo abaixo da primeira versão  utilizada:
```
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


### Gulp
O arquivo `gulpfile.js` é responsável pelas atividades executadas pelo Gulp, veja abaixo o exemplo do gulpfile na primeira versão:
```
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


## Como instalar?


## Como utilizar?
Após a instalação e configuração abra o Gerenciador do Task Runner no Visual Studio e inicie o Gulp.
- abra o diretório `Interface\Estrutura\` no explorer do Visual Studio 

**adicionar pic** - explorer projeto Interface

- clique com o botão direito no arquivo `gulpfile.js`

**adicionar pic** - menu botão direito no gulpfile

- inicie a task `default` no Gerenciador do Task Runner

**adicionar pic** - iniciando a task default no gerenciador do task runner






