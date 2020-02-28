# npm-tutorial

Let's start using npx to create our first react application. 
```
npx create-react-app npm-tutorial
```
Note that npx is an npm package runner, meaning that it will download the package and execute it (npm only downloads packages).

After executing this command, we will have a full react application created, lets investigate whats in the `npm-tutorial` directory.

1. **node_modules**. This is where all the libraries are stored in local. This directory shouldn'd be uploaded to git.
2. **src**. This is where the code of our application lives. Inside there is a bunch of js and css files. All the code in react will be written in js files.
3. **public**. 
4. **package.json**. This file is very important. It is the main file for configuring npm for your application. Everytime you install a new dependency to your project, it will be added to this file. But only the dependencies, but we will have start scripts, build scripts and even, deploy scripts.

## The package.json file
