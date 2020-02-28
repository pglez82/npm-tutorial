# npm-tutorial

Let's start using npx to create our first react application. 
```
npx create-react-app npm-tutorial
```
Note that npx is an npm package runner, meaning that it will download the package and execute it (npm only downloads packages).

After executing this command, we will have a full react application created, lets investigate whats in the `npm-tutorial` directory.

1. **node_modules**. This is where all the libraries are stored in local. This directory shouldn'd be uploaded to git.
2. **src**. This is where the code of our application lives. Inside there is a bunch of js and css files. All the code in react will be written in js files.
3. **public**. Basic resources to load the website.
4. **package.json**. This file is very important. It is the main file for configuring npm for your application. Everytime you install a new dependency to your project, it will be added to this file. But only the dependencies, but we will have start scripts, build scripts and even, deploy scripts.
5. **package-lock.json**. 
6. **.git and .gitignore**. An already configured git repository.

## The package.json file
```json5
  "name": "npm-tutorial",
  "version": "0.1.0",
  "private": true,
```
The first part of the file are the name, the version, and a flag indicating in the package is or not private. private=true means the software is not meant to be published in public repositories. The next section are the dependencies:

```
  "dependencies": {
    "@testing-library/jest-dom": "^4.2.4",
    "@testing-library/react": "^9.4.1",
    "@testing-library/user-event": "^7.2.1",
    "react": "^16.13.0",
    "react-dom": "^16.13.0",
    "react-scripts": "3.4.0"
  },
```
This is the libraries on which we depend. Lets say that we find a library that we want to use, in this case google-map-react. In order to add it to our project we should execute:
```
npm install --save google-map-react
```
This will add a new line to dependencies section:
```
"google-map-react": "^1.1.6",
```
The ^ symbol means that this package will be updated (when available) until there is a major version (in this case until 2.0.0 release). Check this [discussion](https://stackoverflow.com/questions/22343224/whats-the-difference-between-tilde-and-caret-in-package-json) for further information.

We can always update our node_modules directory (or create it if we've just cloned the project) executing `npm install`

The next part are the scripts. This is very important part as it allow us to start the application, build a release version, etc.
```
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

```
  "eslintConfig": { 
    "extends": "react-app"
  },
```
This part is the **linting** configuration. It statically analyzes the code looking for problems or improvements (unused imports, etc).

```
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

## Adding a deploy script
Follow instructions [here](https://dev.to/yuribenjamin/how-to-deploy-react-app-in-github-pages-2a1f)

