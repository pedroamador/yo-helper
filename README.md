# madoos-yo-helper

Allows abstract writing of templates for yeoman generators.

## Getting Started

To install:

    npm i --save madoos-yo-helper

In the generator index:

``` javascript
const yeoman = require('yeoman-generator');

const generatorName = 'madoos-node-module';
const questions = [{type: 'input', name: 'name',message: 'Your project name',default: null}];    
const templatePath = require('path').join(__dirname, './templates');


const yoHelper = require('madoos-yo-helper')(generatorName, questions, templatePath);


module.exports = yeoman.Base.extend({
  prompting: yoHelper.prompts,
  writing: yoHelper.fileWriter, 
  install: function () {
    this.installDependencies();
  }
});
```

If you want to use the yeoman context to get props:

``` javascript
const yeoman = require('yeoman-generator');

const generatorName = 'madoos-node-module';
const questions = function(){
    // Now paquestionsco is a function that allows to obtain the context of yoeman
    const appName = {type: 'input', name: 'name',message: 'Your project name',default: this.appname}
    return [appName];
};
const templatePath = require('path').join(__dirname, './templates');


const yoHelper = require('madoos-yo-helper')(generatorName, questions, templatePath);


module.exports = yeoman.Base.extend({
  prompting: yoHelper.prompts,
  writing: yoHelper.fileWriter, 
  install: function () {
    this.installDependencies();
  }
});
```