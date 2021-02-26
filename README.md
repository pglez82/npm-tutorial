# Starting with NPM
NPM is a software Package Manager and Installer, that will allow us to automate the dependency managment of our Node projects. It also happens to be the largests software repository in the world with more than 800k published packages.

In this example we are going to create a project that uses NPM from scratch:

```
npm init
```
After answering some basic stuff about our project (press enter for default values), a `package.json` file will be created. This file is very important. It is the main file for configuring npm for your application.

Lets say we want to create a simple application that computes the distance between two coordinates. Using a search engine we can find a [library](https://www.npmjs.com/package/geolib) that does just that. Lets just add this dependency to our new project:

```sh
npm install --save geolib
```
Check your `package.json` file. In the dependencies section, you will see geolib. The actual library files will be in the `node_modules` directory.

Lets write a simple program that uses this library. Create a file `index.js`:

```javascript
const geolib = require('geolib');

console.log(geolib.getDistance(
    { latitude: 43.3694855, longitude: -5.8661674 }, //Oviedo
    { latitude: 43.5314231, longitude: -5.7034739 }  //Gijón
));
```
If we execute this program using `node index.js` the result will be `22312`, that is the distance between Oviedo and Gijón in meters. It works!

Lets see how to automate lauching the application. Go to the `package.json` and find the scripts section. Lets write our first script:

```yaml
"scripts": {
   "start": "node index.js"
},
```
Now we can run our application with `npm start`. Obviously we can have more scripts. We will deep more into this in the next example.



# Using NPM to create a basic React application

Let's start using npx to create our first react application. 
```
npx create-react-app npm-tutorial
```
Note that *npx* is an npm package runner, meaning that it will download the package and execute it (npm only downloads packages).

After executing this command, we will have a full react application created, lets investigate whats in the `npm-tutorial` directory.

1. **node_modules**. This is where all the libraries are stored in local. This directory shouldn'd be uploaded to git.
2. **src**. This is where the code of our application lives. Inside there is a bunch of js and css files. All the code in react will be written in js files.
3. **public**. Basic resources to load the website.
4. **package.json**. This file is very important. It is the main file for configuring npm for your application. Everytime you install a new dependency to your project, it will be added to this file. But only the dependencies, but we will have start scripts, build scripts and even, deploy scripts.
5. **package-lock.json**. It has an exact representation of the dependency tree. This is done to ensure that all developers can share the same libraries version. More on this later.
6. **.git and .gitignore**. An already configured git repository.

## The package.json file
```yaml
  "name": "npm-tutorial",
  "version": "0.1.0",
  "private": true,
```
The first part of the file are the name, the version, and a flag indicating in the package is or not private. `private=true` means the software is not meant to be published in public repositories. The next section are the dependencies:

```yaml
  "dependencies": {
    "@testing-library/jest-dom": "^5.11.9",
    "@testing-library/react": "^11.2.5",
    "@testing-library/user-event": "^12.7.3",
    "cra-template": "1.1.2",
    "react": "^17.0.1",
    "react-dom": "^17.0.1",
    "react-scripts": "4.0.3",
    "web-vitals": "^1.1.0"
  },
```
This is the libraries on which we depend. Lets say that we find a library that we want to use, in this case google-map-react. In order to add it to our project we should execute:
```
npm install --save google-map-react
```
This will add a new line to dependencies section:
```yaml
"google-map-react": "^2.1.9",
```
The ^ symbol means that this package will be updated (when available) until there is a major version (in this case until 3.0.0 release). If we use ~, it will update when there is new patch version (version numbers are *major.minor.patch*). Check this [discussion](https://stackoverflow.com/questions/22343224/whats-the-difference-between-tilde-and-caret-in-package-json) for further information.

We can always update our node_modules directory (or create it if we've just cloned the project). There are multiple ways to do that:
* `npm install`. Will install all the packages of `package.json`. It will try to use the specific versions in `package-lock.json`.
* `npm update`. If we have specified versions as *^2.1.9*, it will try to update the versions accordinly and then it will rewrite both `package.json` and `package-lock.json`.
* `npm ci`. Installs the package versions in `package-lock.json`.

A good explanation of the diffference between these commands is in this [post](https://stackoverflow.com/a/53594050/2828454).

There is also the possibility to **delete a dependency**. For that matter use npm uninstall google-map-react --save

The next part are the scripts. This is very important part as it allow us to start the application, build a release version, etc.
```yaml
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
```
So, we have four scripts defined, all of them dependent on the react-scripts package. This is what they do:
* start. It creates a development server in localhost and launch the app in the browser. It supports online modifications.
* build. Minify the application and prepares it optimized for production.
* test. Runs the tests using **jest**.
* eject. Removes the extra layer that create-react-app has created for us to make things simpler and let us configure everything that is under the hood.

We may create more scripts. We will do this in the next section of this tutorial in order automatically deploy our web application to github.io.

```yaml
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
```
This part is the **linting** configuration. It statically analyzes the code looking for problems or improvements (unused imports, etc).

```yaml
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
```
**Browserlist** is a powerful module that handles the problem of the vast number of browsers available in the market. For instance, not all javascript versions are compatible with every browsers. Also some css3 rules must be written with prefixes in order to make them work in multiple browsers. This module lets us define which browsers we are targeting, so modules that work under it (like babel), can share the same configuration. More information [here](https://github.com/browserslist/browserslist).

