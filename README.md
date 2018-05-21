# Learn Angular4

### Introduction
Angular 4 is a full-fledged JavaScript framework for building web applications and apps in JavaScript, html, and TypeScript, which is a superset of JavaScript.The code is written in TypeScript, which compiles to JavaScript and displays the same in the browser.

### Features
* Easy to learn and implement
* Backed by Google
* Nice integration with CSS(Bootstrap & Foundation)
* Two way data binding
* Dependency injection(Separation of layers)
* Post back free(Loading data without refreshing page)

### Prerequisites

* HTML
* CSS
* JAVASCRIPT
* TYPESCRIPT
* PROGRAMMING FUNDAMENTALS

### Software Requirements
* NODEJS
* NPM
* ANGULAR CLI
* IDE (for writing code)


### Installation



```console
Check that if nodejs and npm is installed in your system by running node -v and  npm -v in a terminal/console window.
This will help you to see the version installed in your system.If it does not print anything ,you need to install the package based on your os.
```
**NOTE: Verify that you are running at least Node.js version 8.x or greater and npm version 5.x or greater**

```bash
npm install -g @angular/cli
```

### Usage

```bash
ng help
```

### Generating and serving an Angular project via a development server

```bash
ng new PROJECT-NAME
cd PROJECT-NAME
ng serve  
```

 Navigate to `http://localhost:4200/`.The app will automatically reload if you change any of the source files.
 
You can configure the default HTTP host and port used by the development server with  command-line options :

```bash
ng serve --host 0.0.0.0 --port 4504
```
### npm ERR!registry error parsing json- while trying to install npm in Windows
```bash
npm cache clean
npm config set proxy 'username:password@your.proxy.com'
npm config set https-proxy 'username:password@your.proxy.com'
```
