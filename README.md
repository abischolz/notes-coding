# TYPESCRIPT 

It's like Javascript had a baby with Java. 


>TypeScript code is a superset of JavaScript code—it has all the features of traditional JavaScript but adds some new features.

* Developed by Microsoft
* Meant to bring more structure to Javascript, which is a very flexible language 
* Adds types 

Like Java, Typescript must be processed before it will run (Java: compiled, Typescript: transpiled). It does this since once it runs, its output will be a JS file. 



---

[Transpile](https://en.wikipedia.org/wiki/Source-to-source_compiler) => also known as a source-to-source compiler 

Why is it different from a comiler? 

>A source-to-source translator, source-to-source compiler (S2S compiler), transcompiler, or transpiler is a type of translator that takes the source code of a program written in a programming language as its input and produces an equivalent source code in the same or a different programming language.

vs. 

>...a traditional compiler translates from a higher level programming language to a lower level programming language.



---

### Type inference 

JS 
```
let cat = 9; 
....code code code 

cat = 'Fido';
```
Everything is good, nothing breaks. JS doesn't care. 

TS 
```
let cat = 9; 
....code code code 

cat = 'Fido';

ERROR
Type 'cat' is not assignable to type 'integer'
```
BROKEN. You cannot declare a variable with one data type and then assign the variable a value of a different data type. TS says not today and it will throw an error when transpiling.

New concept alert: shape 

>An object’s shape describes, among other things, what properties and methods it does or doesn’t contain.

This isn't only about objects. This is also referring to the prototype chain - data types of type `string` have access to `.toUpperCase()`, `.length`, etc. If you try to use a method that is not accessible by that data type, TS will let you know. This applies to misspellings and calling a method of the wrong type. 

```
index.ts:3:23 - error TS2551: Property 'toUppercase' does not exist on type 'string'. Did you mean 'toUpperCase'?

3 console.log(firstName.toUppercase());
```

If no initial value is declared, TS classifies this variable of tyep `any`. Variables of type `any` can be reassigned to any data type - not just initially, but indefinitely. 
```
let onOrOff;
 
onOrOff = 1;
onOrOff = false;
```

Don't want this? Use a type annotation. Type annotations use a colon instead of an equal sign. 
```

let mustBeAString : string;
//                  ^ must be a valid data type 

mustBeAString = 'Catdog';
 
mustBeAString = 1337;
// Error: Type 'number' is not assignable to type 'string'
```

### Config files 

It's stored in `tsconfig.json` and can be used to modify some of the default rules of TS. Like all `config` files, it must be at root of project. 

```
{
  "compilerOptions": {
    "target": "es2017",
    "module": "commonjs",
    "strictNullChecks": true
  },
  "include": ["**/*.ts"]
}
```
**What are these options?** (from [CodeAcademy](https://www.codecademy.com/courses/learn-typescript/articles/the-tsconfig-json-file))

* `compilerOptions` - a nested object that contains the rules for the TypeScript compiler to enforce.
    * `target` - specifies which standards of ECMAScript will be followed (i.e. here it is 2017)
    * `module` - specifies module system (here it is CommonJS)
    * `strictNullChecks` - specifies that values `null` or `undefined` must be explicitly assigned 
    * `include` - specifies which files to apply this config to . `["**/*.ts"]` points to all files with a `.ts` extension 

When a `tsconfig.json` is included, it's possible to run `tsc` in the terminal without arguments

### Functions

Functions in JS have parameters, but you can pretty much pass in whatever. 
```
function printLengthOfText(text) {
  console.log(text.length);
}
 
printLengthOfText(3); // Prints: undefined
```
Function runs, but in an unexpected way. JS requires error handling to deal with any unexpected inputs. 

```
function printLengthOfText(text) {
  if (typeof text !== 'string') {
    throw new Error('Argument is not a string!');
  }
 
  console.log(text.length);
}
 
printLengthOfText(3); // Error: Argument is not a string!
```

It's a lot of code. No one likes it. TS does like Java - it declares the type with the parameter. 

```
function greet(name: string) {
  console.log(`Hello, ${name}!`);
}

```
If no type is declared, the parameter will be typed as `any`. 

Sometimes, your parameter is optional - for those cases, use the optional `?`

```
function greet(name?: string) {
  console.log(`Hello, ${name || 'Anonymous'}!`);
}

```

Sometimes parameters have default values - TS has that covered too. It's the same as JS. 

Typescript will also infer the return value. If a variable has already been typed and is assigned to a function that returns a differnt data type, it will not compile (or transpile, whatevs). 

```
function ouncesToCups(ounces: number) {
  return `${ounces / 16} cups`;
}
 
const liquidAmount: number = ouncesToCups(3);
// Type 'string' is not assignable to type 'number'.
```

If you want to be more strict, returns can be explicitly typed. It's the same as Java. 

```
function createGreeting(name?: string): string {
  if (name) {
    return `Hello, ${name}!`;
  }
 
  return undefined;
  //Typescript Error: Type 'undefined' is not assignable to type 'string'.
};
```

**ARROW FUNCTION** 

```

const createArrowGreeting = (name?: string): string => {
    if (name) {
        return `Hello, ${name}!`;
    }
 
    return undefined;
    // Typescript Error: Type 'undefined' is not assignable to type 'string'.
};

```

No return? No problem - do what Java does, type it as `void`

```
function logGreeting(name:string): void{
  console.log(`Hello, ${name}!`)
}
```


ALSO - JSDOCs???? it's native to TS!!! 

How to use: 

```
  /**
   * Returns the sum of two numbers.
   *
   * @param x - The first input number
   * @param y - The second input number
   * @returns The sum of `x` and `y`
   *
   */
  function getSum(x: number, y: number): number {
    return x + y;
  }
```
Reference:
* [Compiler Options](https://www.typescriptlang.org/docs/handbook/compiler-options.html#compiler-options)
* [Intro to the TSConfig Reference](https://www.typescriptlang.org/tsconfig)


###### tags: `general` 