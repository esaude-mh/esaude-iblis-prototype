<br/><br/><br/>
<img src="https://s3-eu-west-1.amazonaws.com/esaude/images/esaude-site-header.png" alt="OpenMRS"/>
<br/><br/><br/>

# iBlis Prototype Point of Care

[![Build Status](https://travis-ci.org/esaude/esaude-iblis-prototype.svg?branch=master)](https://travis-ci.org)
[![Coverage Status](https://coveralls.io/repos/github/esaude/esaude-iblis-prototype/badge.svg?branch=master)](https://coveralls.io/github/esaude/esaude-iblis-prototype?branch=master)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/f5c045d801c54cddad7a5c049e6def3c)](https://www.codacy.com/app/larslemos/esaude-iblis-prototype?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=esaude/esaude-iblis-prototype&amp;utm_campaign=Badge_Grade)
[![Test Coverage](https://api.codacy.com/project/badge/coverage/10ea6c2d88674139b37cae5fa73cc8f6)](https://)
[![Dependency Status](https://gemnasium.com/badges/github.com/esaude/esaude-iblis-prototype.svg)](https://gemnasium.com/github.com/esaude/esaude-iblis-prototype)

[![eSaude Version](https://omrs-shields.psbrandt.io/custom/esaude/v1.2.0/brightgreen?logo=esaude)](http://)

[![eSaude Slack](https://slack.esaude.org/badge.svg)](https://slack.esaude.org)

This project is an AngularJS application for point of care based on iBLIS and using
The UI was designed for tablet-like interfaces with touch screen and virtual keyboard.

A demo of the system can be found [here](https://iblis.esaude.org/).

A development demo of the system can be found   [here](https://esaude-iblis.herokuapp.com/).

The back-end system of iBLIS can be found [here](https://iblis-old.esaude.org).

## Setup (Development Environment)

## Prerequisites

1. Install [Node.js](http://nodejs.org)

3. Install these NPM packages globally

    ```bash
    npm install -g bower gulp nodemon
    ```


### Linting
 - Run code analysis using `gulp vet`. This runs jshint, jscs, and plato.

### Tests
 - Run the unit tests using `gulp test` (via karma, mocha, sinon).

### Running in dev mode
 - Run the project with `gulp serve-dev`

 - opens it in a browser and updates the browser with any files changes.

### Building the project
 - Build the optimized project using `gulp build`
 - This create the optimized code for the project and puts it in the build folder

### Running the optimized code
 - Run the optimize project from the build folder with `gulp serve-build`

### Structure
The structure also contains a gulpfile.js and a server folder. The server is there just so we can serve the app using node. Feel free to use any server you wish.

	/src
		/client
			/app
			/content

### Installing Packages
When you generate the project it should run these commands, but if you notice missing packages, run these again:

 - `npm install`
 - `bower install`

### The Modules
The app has 5 feature modules and depends on a series of external modules and custom but cross-app modules

```
app --> [
        app.admin,
        app.dashboard
        app.patients,
        app.tests,
                        --> [
                        app.core,
                        app.widgets
                    ],
        app.layout --> [
            app.core
        ],
        app.widgets,
    		app.core --> [
    			ngAnimate,
    			ui.router,
          ngSanitize,
    			blocks.exception,
    			blocks.logger,
    			blocks.router
    		],

    ]
```

##### blocks.logger Module
The `blocks.logger` module handles logging across the Angular app.

##### blocks.exception Module
The `blocks.exception` module handles exceptions across the Angular app.

It depends on the `blocks.logger` module, because the implementation logs the exceptions.

##### blocks.router Module
The `blocks.router` module contains a routing helper module that assists in adding routes to the $routeProvider.

## Gulp Tasks

### Task Listing

- `gulp help`

    Displays all of the available gulp tasks.

### Code Analysis

- `gulp vet`

    Performs static code analysis on all javascript files. Runs jshint and jscs.

- `gulp vet --verbose`

    Displays all files affected and extended information about the code analysis.

- `gulp plato`

    Performs code analysis using plato on all javascript files. Plato generates a report in the reports folder.

### Testing

- `gulp serve-specs`

    Serves and browses to the spec runner html page and runs the unit tests in it. Injects any changes on the fly and re runs the tests. Quick and easy view of tests as an alternative to terminal via `gulp test`.

- `gulp test`

    Runs all unit tests using karma runner, mocha, chai and sinon with phantomjs. Depends on vet task, for code analysis.

- `gulp test --startServers`

    Runs all unit tests and midway tests. Cranks up a second node process to run a server for the midway tests to hit a web api.

- `gulp autotest`

    Runs a watch to run all unit tests.

- `gulp autotest --startServers`

    Runs a watch to run all unit tests and midway tests. Cranks up a second node process to run a server for the midway tests to hit a web api.

### Cleaning Up

- `gulp clean`

    Remove all files from the build and temp folders

- `gulp clean-images`

    Remove all images from the build folder

- `gulp clean-code`

    Remove all javascript and html from the build folder

- `gulp clean-fonts`

    Remove all fonts from the build folder

- `gulp clean-styles`

    Remove all styles from the build folder

### Fonts and Images

- `gulp fonts`

    Copy all fonts from source to the build folder

- `gulp images`

    Copy all images from source to the build folder

### Styles

- `gulp styles`

    Compile less files to CSS, add vendor prefixes, and copy to the build folder

### Bower Files

- `gulp wiredep`

    Looks up all bower components' main files and JavaScript source code, then adds them to the `index.html`.

    The `.bowerrc` file also runs this as a postinstall task whenever `bower install` is run.

### Angular HTML Templates

- `gulp templatecache`

    Create an Angular module that adds all HTML templates to Angular's $templateCache. This pre-fetches all HTML templates saving XHR calls for the HTML.

- `gulp templatecache --verbose`

    Displays all files affected by the task.

### Serving Development Code

- `gulp serve-dev`

    Serves the development code and launches it in a browser. The goal of building for development is to do it as fast as possible, to keep development moving efficiently. This task serves all code from the source folders and compiles less to css in a temp folder.

- `gulp serve-dev --nosync`

    Serves the development code without launching the browser.

- `gulp serve-dev --debug`

    Launch debugger with node-inspector.

- `gulp serve-dev --debug-brk`

    Launch debugger and break on 1st line with node-inspector.

### Building Production Code

- `gulp optimize`

    Optimize all javascript and styles, move to a build folder, and inject them into the new index.html

- `gulp build`

    Copies all fonts, copies images and runs `gulp optimize` to build the production code to the build folder.

### Serving Production Code

- `gulp serve-build`

    Serve the optimized code from the build folder and launch it in a browser.

- `gulp serve-build --nosync`

    Serve the optimized code from the build folder and manually launch the browser.

- `gulp serve-build --debug`

    Launch debugger with node-inspector.

- `gulp serve-build --debug-brk`

    Launch debugger and break on 1st line with node-inspector.

### Bumping Versions

- `gulp bump`

    Bump the minor version using semver.
    ```
    --type=patch // default
    --type=minor
    --type=major
    --type=pre
    --ver=1.2.3 // specific version

## License
MIT
