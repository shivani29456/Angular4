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
* IDE (for writing code and to code quickly install `typescript` package.)

### Angular CLI (Command Line Interface)- Introduction

Angular provides an utility to allow users to create and manage projects from the command line. It automates tasks like creating projects, adding new controllers, etc. It’s generally a good idea to use angular-cli as it will help create and maintain common patterns across our application and use **scaffolding** for easier development workflows.

### What is scaffolding?

The CLI tool has commands for scaffolding. This makes it possible to add things like new components, routes or services from the command line. People who have worked with other frameworks such as Ruby on Rails will be familiar with this.
To use scaffolding the ng generate or ng g command is used. Some of the things that can be added with scaffolding are components, routes, services, classes and pipes.
Apart from speeding up development, scaffolding will also enforce a strict project structure. This helps when collaborating with other developers and makes it easier to navigate projects written by other people.

### Installation



```console
Check that if nodejs and npm is installed in your system by running node -v and  npm -v in a terminal/console window.
This will help you to see the version installed in your system.If it does not print anything ,you need to install the package based on your os.
```
**NOTE: Verify that you are running at least Node.js version 8.x or greater and npm version 5.x or greater**

```bash
npm install -g @angular/cli
```
This installs angular-cli globally on your system.

If you’ve already installed a former version of angular-cli you need to execute the following command sequence:
```bash
npm uninstall -g angular-cli
npm cache clean
npm install -g angular-cli@latest
```
![alt text](https://cli.angular.io/images/cli-logo.svg)

### Usage

```bash
ng help
```

### Generating and serving an Angular project via a development server

```bash
ng new my-dream-app
cd my-dream-app
ng serve  
```

 Navigate to `http://localhost:4200/`.The app will automatically reload if you change any of the source files.
 
You can configure the default HTTP host and port used by the development server with  command-line options :

```bash
ng serve --host 0.0.0.0 --port 4504
```

### Generating Components, Directives, Pipes and Services

You can use the ng generate (or just ng g) command to generate Angular components:

| **Scaffold**| **Usage** |
| --- | --- |
| Component | ng g component my-new-component |
| Directive | ng g directive my-new-directive |
| Pipe | ng g directive my-new-pipe |
| Service | ng g directive my-new-service |
| Class | ng g directive my-new-class |


### npm ERR!registry error parsing json- while trying to install npm in Windows
```bash
npm cache clean
npm config set proxy 'username:password@your.proxy.com'
npm config set https-proxy 'username:password@your.proxy.com'
```

### Why do we need installation of both global and local version of Angular CLI ??

The global install is needed to start a new application. The ```ng new <app-name>``` command is run using the global installation of the CLI. In fact, if you try to run ng new while inside the folder structure of an existing CLI application, you get this lovely error:
```console 
You cannot use the new command inside an Angular CLI project.
```
Other commands that can be run from the global install are ```ng help```, ```ng get/set``` with the --global option, ```ng version```, ```ng doc```, and ```ng completion```.
The local install of the CLI is used after an application has been built. This way, when new versions of the CLI are available, you can update your global install, and not affect the local install. This is good for the stability of a project. Most ng commands only make sense with the local version, like ```lint```, ```build``` and ```serve```, etc.
### How to fix this warning:-
```console
Your global Angular CLI version (1.1.1) is greater than your local version (1.0.6). The local Angular CLI version is used.
```
```bash
npm uninstall --save-dev angular-cli
npm install --save-dev @angular/cli@latest
npm install
```


### PDF Creation using JSPDF

JSON Data(Birds.json)
```bash
[
{
    "ID": "001",
   "Name": "Eurasian Collared-Dove",
    "Type": "Dove",
    "Scientific Name": "Streptopelia"
},
{
    "ID": "002",
    "Name": "Bald Eagle",
    "Type": "Hawk",
    "Scientific Name": "Haliaeetus leucocephalus" 
},
{
    "ID": "003",
    "Name": "Cooper's Hawk",
    "Type": "Hawk",
    "Scientific Name": "Accipiter cooperii" 
}
]
```
* Step 1:
   - **app.module.ts**:- ``` import { HttpClientModule } from '@angular/common/http'; ```
* Step 2:
   -**app.component.ts**:-
```bash
import { Component, ViewChild, ElementRef } from '@angular/core';
import * as jsPDF from 'jspdf';
import { HttpClient } from '@angular/common/http';
import { HttpErrorResponse } from '@angular/common/http';
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
 // title = 'app';
@ViewChild('content') content:ElementRef;
 title = 'JSON to Table Example';
  constructor (private httpService: HttpClient) { }
  arrBirds: string [];

  ngOnInit () {
    this.httpService.get('./assets/Birds.json').subscribe(
      data => {
        this.arrBirds = data as string [];	 // FILL THE ARRAY WITH DATA.
        //  console.log(this.arrBirds[1]);
      },
      (err: HttpErrorResponse) => {
        console.log (err.message);
      }
    );
  }

public downloadPDf(){
	let doc=new jsPDF();
	let specialElementHandlers = {
	'#editor' : function(element,renderer) {
          return true;
	}
	};


	let content=this.content.nativeElement;
	doc.fromHTML(content.innerHTML,15,15 ,{
	'width':190,
	'elementHandlers':specialElementHandlers
	});
	doc.save('xxx.pdf');
}
}
```
* Step3:-
   - **app.component.html**:-
```bash
<div id="content" #content style="text-align:left;width:auto;">

    <h1>
        {{ title }}!
    </h1>

    <table *ngIf="arrBirds  " width="100%" style="font-size:9px;" >
        <!-- ADD HEADERS -->
        <tr >
            <th>ID</th>
                <th>Name</th>
                <th>Type</th>

        </tr>

        <!-- BIND ARRAY TO TABLE -->
        <tr *ngFor="let bird of arrBirds" hidden="true">
            <td>{{bird.ID}}</td>
                <td>{{bird.Name}}</td>
                    <td>{{bird.Type}}</td>
        </tr>
    </table>
</div>

<button (click)="downloadPDf()">Export to Pdf</button>
```
* Step 4:-(for styling purpose)
  - **app.component.css**:-
```bash
table, th, td 
{
    margin: 10px 0;
    
    padding: auto;
    font: 15px Verdana;
    visibility: hidden;

}
th {
    font-weight:bold;
    visibility: hidden;
}
tr{
	visibility: hidden;
}
```
**Output**:-

| ID | Name | Type |
| :---         |     :---      |          :--- |
| 001   |Eurasian Collared-Dove     | Dove    |
| 002     | Bald Eagle       | Hawk     |
| 003     | Cooper's Hawk       | Hawk     |


**Optional**

* Step 5:-
  - Set the tabel header and adjust its fontsize :- ``` doc.setFontSize(30);
    doc.text(460, 70, "Daily Contribution Report",'center'); ```


## MultiChart ([ref])(http://krispo.github.io/angular-nvd3/)

![alt text](http://krispo.github.io/angular-nvd3/img/multiChart.png)
```bash
{
  "chart": {
    "type": "multiChart",
    "height": 450,
    "margin": {
      "top": 30,
      "right": 60,
      "bottom": 50,
      "left": 70
    },
    "color": [
      "#1f77b4",
      "#ff7f0e",
      "#2ca02c",
      "#d62728",
      "#9467bd",
      "#8c564b",
      "#e377c2",
      "#7f7f7f",
      "#bcbd22",
      "#17becf"
    ],
    "duration": 500,
    "xAxis": {
      "dispatch": {},
      "axisLabelDistance": 0,
      "staggerLabels": false,
      "rotateLabels": 0,
      "rotateYLabel": true,
      "showMaxMin": true,
      "axisLabel": null,
      "height": 60,
      "ticks": null,
      "width": 75,
      "margin": {
        "top": 0,
        "right": 0,
        "bottom": 0,
        "left": 0
      },
      "duration": 250,
      "orient": "bottom",
      "tickValues": null,
      "tickSubdivide": 0,
      "tickSize": 6,
      "tickPadding": 5,
      "domain": [
        0,
        1
      ],
      "range": [
        0,
        1
      ]
    },
    "yAxis1": {
      "dispatch": {},
      "axisLabelDistance": 0,
      "staggerLabels": false,
      "rotateLabels": 0,
      "rotateYLabel": true,
      "showMaxMin": true,
      "axisLabel": null,
      "height": 60,
      "ticks": null,
      "width": 75,
      "margin": {
        "top": 0,
        "right": 0,
        "bottom": 0,
        "left": 0
      },
      "duration": 250,
      "orient": "left",
      "tickValues": null,
      "tickSubdivide": 0,
      "tickSize": 6,
      "tickPadding": 3,
      "domain": [
        0,
        1
      ],
      "range": [
        0,
        1
      ]
    },
    "yAxis2": {
      "dispatch": {},
      "axisLabelDistance": 0,
      "staggerLabels": false,
      "rotateLabels": 0,
      "rotateYLabel": true,
      "showMaxMin": true,
      "axisLabel": null,
      "height": 60,
      "ticks": null,
      "width": 75,
      "margin": {
        "top": 0,
        "right": 0,
        "bottom": 0,
        "left": 0
      },
      "duration": 250,
      "orient": "right",
      "tickValues": null,
      "tickSubdivide": 0,
      "tickSize": 6,
      "tickPadding": 3,
      "domain": [
        0,
        1
      ],
      "range": [
        0,
        1
      ]
    }
```
## Documentation

Docs can be found [here](https://angular.io/).
