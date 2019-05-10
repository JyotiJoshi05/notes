# Typescript
In programming language design, a first-class citizen (also type, object, entity, or value) in a given programming language is First Class Citizen - an entity which supports all the operations generally available to other entities.
ECMAScript is a standard, JavaScript is an implementation of that standard. 

### TypeScript unique features:
- static typing (can be validated real-time in IDE)
- interfaces/types (including Union, Intersection and special types like Enum)
- generics
- abstract classes
- members visibility (public, private, protected)
- parameter properties (!)
- decorators that already work

### Features of TypeScript:
TypeScript Code is converted into Plain JavaScript Code:: TypeScript code is not understandable by the browsers. Thats why if the code is written in TypeScript then it is compiled and converted the code i.e. translate the code into JavaScript.The above process is known as Trans-piled. By the help of JavaScript code, browsers are able to read the code and display.
JavaScript is TypeScript: Whatever code is written in JavaScript can be converted to TypeScript by changing the extension from .js to .ts.
Use TypeScript anywhere: TypeScript code can be run on any browser, devices or in any operating system. TypeScipt is not specific to any Virtual-machine etc.
TypeScript supports JS libraries: With TypeScript, developers can use existing JavaScript code, incorporate popular JavaScript libraries, and can be called from other JavaScript code.

### Difference between TypeScript and JavaScript:
TypesScript is known as Object oriented programming language whereas JavaScript is a scripting language.
TypeScript has a feature known as Static typing but JavaScript does not have this feature.
TypeScript gives support for modules whereas JavaScript does not support modules.
TypeScript has Interface but JavaScript does not have Interface.
TypeScript support optional parameter function but JavaScript does not support optional parameter function.

### Advantages of using TypeScript over JavaScript
TypeScript always point out the compilation errors at the time of development only. Because of this at the run-time the chance of getting errors are very less whereas JavaScript is an interpreted language.
TypeScript has a feature which is strongly-typed or supports static typing. That means Static typing allows for checking type correctness at compile time. This is not available in JavaScript.
TypeScript is nothing but JavaScript and some additional features i.e. ES6 features. It may not be supported in your target browser but TypeScript compiler can compile the .ts files into ES3,ES4 and ES5 also.

### Disadvantages of using TypeScript over JavaScript
Generally TypeScript takes time to compile the code.
TypeScript does not support abstract classes.

### tsconfig
TypeScript is a primary language for Angular application development. It is a superset of JavaScript with design-time support for type safety and tooling.
Browsers can't execute TypeScript directly. Typescript must be "transpiled" into JavaScript using the tsc compiler, which requires some configuration.

### noImplicitAny and suppressImplicitAnyIndexErrors
TypeScript developers disagree about whether the noImplicitAny flag should be true or false. There is no correct answer and you can change the flag later. But your choice now can make a difference in larger projects, so it merits discussion.

When the noImplicitAny flag is false (the default), and if the compiler cannot infer the variable type based on how it's used, the compiler silently defaults the type to any. That's what is meant by implicit any.

The documentation setup sets the noImplicitAny flag to true. When the noImplicitAny flag is true and the TypeScript compiler cannot infer the type, it still generates the JavaScript files, but it also reports an error. Many seasoned developers prefer this stricter setting because type checking catches more unintentional errors at compile time.

You can set a variable's type to any even when the noImplicitAny flag is true.

When the noImplicitAny flag is true, you may get implicit index errors as well. Most developers feel that this particular error is more annoying than helpful. You can suppress them with the following additional flag:

"suppressImplicitAnyIndexErrors":true

### Typings

Many JavaScript libraries, such as jQuery, the Jasmine testing library, and Angular, extend the JavaScript environment with features and syntax that the TypeScript compiler doesn't recognize natively. When the compiler doesn't recognize something, it throws an error.

Use TypeScript type definition files—d.ts files—to tell the compiler about the libraries you load.

TypeScript-aware editors leverage these same definition files to display type information about library features.

Many libraries—jQuery, Jasmine, and Lodash among them—do not include d.ts files in their npm packages. Fortunately, either their authors or community contributors have created separate d.ts files for these libraries and published them in well-known locations.

You can install these typings via npm using the @types/* scoped package and Typescript, starting at 2.0, automatically recognizes them