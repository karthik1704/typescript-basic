# TypeScipt

## What is TypeScript?

- TypeScript is **Superset** of JavaScript.

  - Build Up on JS
  - Adds new features + advantages to JS
  - TS code compile to JS code(Vanila Js)
  - You can write JS code in TS file
  - **Featues**

    - Types (Data Type Control)
    - Better error handling(compare js)
    - Interface or Generics (Non-JS features)
    - Decorators (Mata-Programming Features)
    - Rich Configuration Options

- Cons:

  - Browser Can't execute Ts ( Browser not support TS)

**Example**:

```typescript
//app.ts
function add(num1: number, num2: number) {
  return num1 + num2;
}
```

**Compile**

```cmd
> tsc ./app.ts
```

## TypeScript Basics

### Working with Types

- Core Types

  - number (All Numbers , no different btw int or floats)
  - string ('HI',"HI",\`Hi\`)
  - boolean (T or F / 0 or 1)
  - object ( {age: 20} )
  - Array [1,2,3]
  - Tuple [1,2] - added by TS: Fixed-length & Fixed-Type array
  - Enum enum{NEW, OLD} - added by TS - automatically enumerated global constant identifiers
  - Any (\*) - any kind of value , no specific type assignment

### Basic Data Types

```ts
// core Data Type
function add(n1: number, n2: number, showResult: boolean, phrase: string) {
  consloe.log(typeof n1); // logs number
  const result = n1 + n2;
  if (showResult) {
    console.log(pharse + result);
  } else {
    return result;
  }
}

const number1 = 5; //number
const number2 = 2.8; // folats aslo number
const printResult = true; //boolean
const resultPhrase = "Result is: "; // string

// or you can expilicitly assign data type to variable
// but TS automatically detects datatype with inital value
// and  its not good pratices ,

// const number1: number = 5; //number
// const number2: number = 2.8; // folats aslo number
// const printResult: boolean = true; //boolean
// const resultPhrase: string = "Result is: "; // string

// but only define variable
let number3: number; // its good pratices
let number4; // without datatype -> TS consider any datatype (number4:any )
//later
number3 = 6;

add(number1, number2, printResult, resultPhrase);
```

### Objects

```ts
const person = {
  name: "Karthi",
  age: 24,
};

// or
// const person {
//   name: string;
//   age: number;
// } = {
//   name: 'Karthi',
//   age: 24
// }
// but typescript detects so no need for this
```

### Array

```ts
const person = {
  name: 'Karthi',
  age: 24
  hobbies: ['Games','Eating'] ,  // Ts Detects hobbies: string[]
}

let favActivities: string[]; // array of string
favActivities = ['sports'];

```

### Tuple

```ts

const person:{
  name: string;
  age: number;
  hobbies: string[];
  role: [number,string] // tuple , we have to override data type to assign tuple
} = {
  name: 'Karthi',
  age: 24
  hobbies: ['Games','Eating'] ,
  role: [2, 'author'],
}
// carefull with push
```

### Enum

```ts
// enum naming convention start with uppercase
// moslty enum values uppercase , that's not must-do
enum Role {ADMIN, READ_ONLY, AUTHOR};
// compiled emnum have ADMIN=0... if don't start with 0
//enum Role {ADMIN = 5, READ_ONLY, AUTHOR};
// also strings enum Role {ADMIN = 'ADMIN' , READ_ONLY = 100, AUTHOR};

const person = {
  name: 'Karthi',
  age: 24
  hobbies: ['Games','Eating'] ,
  role: Role.ADMIN
}

```

### Any

```ts
// avoid any moslty
let favActivities: any;
favActivities = 5;
//or
favActivities = ["doe"];

let favActivities: any[]; // its show its any array
favActivities = ["sports", 4, , "games"];
```

## Union

```ts
//two different type of data wants to use same fn, variable  then use union
//
function combine(n1: number | string, n2: number | string) {
  let result;
  if (typeof n1 === "number" && typeof n2 === "number") {
    const result = n1 + n2;
  } else {
    const result = n1.toString() + n2.toString();
  }
  return result;
}

const combinedAges = combine(30, 26);

const combinedNames = combine("karthi", " A");
```

## Literal

```ts
//  resultConversion: 'as-number' | 'as-text' -> literal with union
function combine(
  n1: number | string,
  n2: number | string,
  resultConversion: "as-number" | "as-text"
) {
  let result;
  if (
    (typeof n1 === "number" && typeof n2 === "number") ||
    resultConversion === "as-number"
  ) {
    const result = +n1 + +n2;
  } else {
    const result = n1.toString() + n2.toString();
  }
  return result;
}

const combinedAges = combine(30, 26, "as-number");

const combinedStringAges = ("30", "26", "as-number");

const combinedNames = combine("karthi", " A", "as-text");
```

## Type-Alias

```ts
type Combinable = number | string;
type ConversionDescriptor = "as-number" | "as-text";
function combine(
  n1: Combinable,
  n2: Combinable,
  resultConversion: ConversionDescriptor
) {
  let result;
  if (
    (typeof n1 === "number" && typeof n2 === "number") ||
    resultConversion === "as-number"
  ) {
    const result = +n1 + +n2;
  } else {
    const result = n1.toString() + n2.toString();
  }
  return result;
}

const combinedAges = combine(30, 26, "as-number");

const combinedStringAges = ("30", "26", "as-number");

const combinedNames = combine("karthi", " A", "as-text");
```

## Functions

```ts
// return type
function add(n1: number, n2: number): number {
  return n1 + n2;
}

function result(num: number): void {
  // don't need for return
  console.log("Result: " + num);
}

// function result(num: number): undefined {
//   console.log("Result: " + num);
//   return;
// }

result(add(5, 7));
```

### Function-Type

```ts
let combineValues: Function; // -> ts fn data type
//or if you want args or return type -> funtion type
let combineValues: (a: number, b: number) => number; //-> fn type

combineValues = add; // add is fn
// fn-type with call back
addAndHandle(n1: number, n2: number, cb: (num)=>void){
  const total = n1 + n2;
  cb(total);
}

addAndHandle(10,20,(result)=>{
  console.log(result)
});
console.log(combineValues(8, 8));
```

## Unknown

```ts
let userInput: unknown; // it's any hold value, unknown restricted
let userName: string;

userInput = 6;
userInput = "kkkkjk";

// userName = userInput;  -> throws error, you can't directly assign unknown varible

if (typeof userInput === "string") {
  userName = userInput;
}

// unknown better than any
```

## Never

```ts
// never is funtion type
function generateError(message: string, code: number): never {
  throw { message: message, errorCode: code };
}
// never - moslty used for error (throw)
```

## TypeScript Complier

```cmd
>tsc app.ts --watch
--watch or (-w) -> if changes detected , automatically compile ts file
```

## More than one ts file

```cmd
> tsc --init
this tells this is typescript project and created tsconfig.json

> tsc
or
> tsc -w
// this will complie all ts file in this project
```

### tsconfig.json

- see file named tsconfig.json

### Exclude Inculde Files

```json
{
  "compilerOptions": {
    /* Basic Options */
    // "incremental": true,                   /* Enable incremental compilation */
    "target": "es5" /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017', 'ES2018', 'ES2019' or 'ESNEXT'. */,
    "module": "commonjs" /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', or 'ESNext'. */
    //....
  },

  "exclude": [
    "analytics.ts",
    "*.test.ts",
    "**/*.test.ts ", // any folder , *.test.ts file ignored
    "node_modules" // mostly we exclude node_modules and would be the default mostly
  ],

  "include": ["app.ts", "*.test.ts", "src"]
}
```
