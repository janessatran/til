# Modules(ES6)


## Questions/Topics Covered:
- [Vocabulary: npm, modules, bundler, webpack?](#modules-vocab)
- [How does webpack work?](#webpack)
- [What are modules in ES6?](#modules)
- [What are benefits to using modules?](#modules-benefits)


<h4 id="modules-vocab">
  Define the following:
</h4>
- **npm**: stands for "Node Package Manager". It is a command line tool that gives you access to a repository of plugins, libraries, and tools you can use in your projects. It helps us update/download JS packages for our projects.
- **modules**: bits of code that we can re-use by importing/exporting into other files.
- **bundler**: a tool that finds all the modules (using the `import` or `require` syntax which) and replaces them with the content of the actual file before building
- **webpack**: a module bundler. 

<h4 id="webpack">
  How does webpack work?
</h4>
When webpack runs, it goes through all of our files looking for any `import` statements and then compiles all the code we need to run our site into a single file inside the `dist` folder. 

You run webpack by using the command `npx webpack`.

When we set up our project, the `src` directory is where we write all of the code that webpack will bundle for us. Our **entry** file is the main application file that links to all the other modules in the project. In this example, it is the `/src/index.js` file. The **output** file is the compiled version, `/dist/main.js`

```
ebpack-demo
  |- package.json
+ |- webpack.config.js
  |- /dist
    |- index.html
    |+ main.js
  |- /src
    |- index.js
```
<h4 id="modules">
  What are modules in ES6?
</h4>
Essentially it is a bit of code written in a JavaScript file that you can import and export to other files. 

For example:
```javascript
// a file called functionOne.js
const functionOne = () => console.log("FUNCTION ONE!");

export { functionOne }
```

```javascript
//another JS file
import { functionOne } from './functionOne'

functionOne() // this will print out FUNCTION ONE!
```


<h4 id="modules-benefits">
  What are benefits to using modules?
</h4>
1. Code reuse - you can copy a file and re-use it another.
2. Separate code by functionality, which makes writing and maintaining the code much easier and less error-prone.
