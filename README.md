# Getting started with TypeScript

## Section 1.1: Installation and setup

- TypeScript is a typed superset of JavaScript that compiles directly to JavaScript code. 
- TypeScript files commonly use the .ts extension. 
- Many IDEs support TypeScript without any other setup required, but TypeScript can also be compiled with the TypeScript Node.JS package from the command line.

### IDEs

#### Visual Studio

- visual studio 2015 includes Typescript.

#### Visual Studio Code

- Visual Studio Code (vscode) provides contextual autocomplete as well as refactoring and debugging tools for TypeScript.
- vscode is itself implemented in TypeScript. Available for Mac OS X, Windows and Linux.

#### WebStorm

- WebStorm 2016.2 comes with TypeScript and a built-in compiler. [WebStorm is not free]

#### IntelliJ IDEA

- IntelliJ IDEA 2016.2 has support for TypeScript and a compiler via a plugin maintained by the JetBrains team. [IntelliJ is not free]

#### Atom & atom-typescript

- Atom supports TypeScript with the atom-typescript package.

#### Sublime Text

- Sublime Text supports TypeScript with the TypeScript package.

### Installing the command line interface

* Install Node.js

#### Install the npm package globally

You can install TypeScript globally to have access to it from any directory.

```sh
npm install -g typescript
```

or

#### Install the npm package locally

You can install TypeScript locally and save to package.json to restrict to a directory.

```sh
npm install typescript --save-dev Installation channels
```

You can install from:

- Stable channel: npm install typescript
- Beta channel: npm install typescript@beta
- Dev channel: npm install typescript@next

#### Compiling TypeScript code

The tsc compilation command comes with typescript, which can be used to compile code.

```sh
tsc my-code.ts
```

This creates a my-code.js file.

#### Compile using tsconfig.json

- You can also provide compilation options that travel with your code via a tsconfig.json file.
- To start a new TypeScript project, cd into your project's root directory in a terminal window and run tsc --init.
- This command will generate a tsconfig.json file with minimal configuration options, similar to below.

```sh
{
    "compilerOptions": {
        "module": "commonjs",
        "target": "es5",
        "noImplicitAny": false,
        "sourceMap": false,
        "pretty": true
    },
    "exclude": [
        "node_modules"
    ]
}
```

With a tsconfig.json file placed at the root of your TypeScript project, you can use the tsc command to run the compilation.

## Section 1.2: Basic syntax

TypeScript is a typed superset of JavaScript, which means that all JavaScript code is valid TypeScript code. TypeScript adds a lot of new features on top of that.

- TypeScript makes JavaScript more like a strongly-typed, object-oriented language akin to C# and Java.
- This means that TypeScript code tends to be easier to use for large projects and that code tends to be easier to understand and maintain.
- The strong typing also means that the language can (and is) precompiled and that variables cannot be assigned values that are out of their declared range.
- For instance, when a TypeScript variable is declared as a number, you cannot assign a text value to it.


This strong typing and object orientation makes TypeScript **easier to debug and maintain**, and those were two of the weakest points of standard JavaScript.

### Type declarations

You can add type declarations to variables, function parameters and function return types. The type is written after a colon following the variable name, like this: var num: number = 5; The compiler will then check the types (where possible) during compilation and report type errors.

```sh
var num: number = 5;
num = "this is a string"; // error: Type 'string' is not assignable to type 'number'.
```

The basic types are :

- number (both integers and floating point numbers)
- string
- boolean
- Array. You can specify the types of an array's elements. There are two equivalent ways to define array types: Array<T> and T[]. For example:
    - number[] - array of numbers
    - Array<string> - array of strings
- Tuples. Tuples have a fixed number of elements with specific types.
    - [boolean, string] - tuple where the first element is a boolean and the second is a string.
    - [number, number, number] - tuple of three numbers.
-  {} - object, you can define its properties or indexer
    - {name: string, age: number} - object with name and age attributes
    - {[key: string]: number} - a dictionary of numbers indexed by string
- enum -\ { Red = 0, Blue, Green } -\ enumeration mapped to numbers Function. You specify types for the parameters and return value:
    - (param: number) => string - function taking one number parameter returning string
    - () => number - function with no parameters returning an number.
    - (a: string, b?: boolean) => void - function taking a string and optionally a boolean with no return value.
- any - Permits any type. Expressions involving any are not type checked.
- void - represents "nothing", can be used as a function return value. Only null and undefined are part of the void type.
- never
    - let foo: never; -As the type of variables under type guards that are never true.
    - function error(message: string): never { throw new Error(message); } - As the return type of functions that never return.
- null - type for the value null. null is implicitly part of every type, unless strict null checks are enabled.


### Casting

You can perform explicit casting through angle brackets, for instance:

```ts
let derived: MyInterface;
(<ImplementingClass>derived).someSpecificMethod();
```

- This example shows a derived class which is treated by the compiler as a MyInterface. 
- Without the casting on the second line the compiler would throw an exception as it does not understand someSpecificMethod(), but casting through <ImplementingClass>derived suggests the compiler what to do.

Another way of casting in TypeScript is using the as keyword:

```ts
let derived: MyInterface;
(derived as ImplementingClass).someSpecificMethod();
```

Since TypeScript 1.6, the default is using the as keyword, because using <> is ambiguous in .jsx files. This is mentioned in [TypeScript official documentation](https://github.com/Microsoft/TypeScript/wiki/What%27s-new-in-TypeScript#new-tsx-file-extension-and-as-operator).

### Classes

Classes can be defined and used in TypeScript code. To learn more about classes, see the Classes documentation page.

## Section 1.3: Hello World

```ts
class Greeter {
      greeting: string;
constructor(message: string) {
      this.greeting = message;
    }
    greet(): string {
    return this.greeting;
  }
};
```

```ts
let greeter = new Greeter("Hello, world!");
console.log(greeter.greet());
```

- Here we have a class, Greeter, that has a constructor and a greet method.
- We can construct an instance of the class using the new keyword and pass in a string we want the greet method to output to the console.
- The instance of our Greeter class is stored in the greeter variable which we then use to call the greet method.

## Section 1.4: Running TypeScript using ts-node

[ts-node](https://www.npmjs.com/package/ts-node) is an npm package which allows the user to run typescript files directly, without the need for precompilation using tsc. It also provides [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop).

Install ts-node globally using

```sh
npm install -g ts-node
```

ts-node does not bundle typescript compiler, so you might need to install it.

```sh
npm install -g typescript
```

### Executing script

To execute a script named main.ts, run

```sh
ts-node main.ts
```

```sh
// main.ts
console.log("Hello world");
```

Example usage

```sh
$ ts-node main.ts
Hello world
```

### Running REPL

To run REPL run command ts-node

Example usage

```sh
$ ts-node
> const sum = (a, b): number => a + b; undefined
> sum(2, 2)
4
> .exit
```

To exit REPL use command .exit or press CTRL+C twice.

----------------

# Why and when to use TypeScript

If you find the arguments for type systems persuasive in general, then you'll be happy with TypeScript.

It brings many of the advantages of type system (safety, readability, improved tooling) to the JavaScript ecosystem. It also suffers from some of the drawbacks of type systems (added complexity and incompleteness).


## Section 2.1: Safety

TypeScript catches type errors early through static analysis:

```ts
function double(x: number): number {
  return 2 * x;
}
double('2');
// ~~~ Argument of type '"2"' is not assignable to parameter of type 'number'.
```

## Section 2.2: Readability

TypeScript enables editors to provide contextual documentation:

![example](https://i.stack.imgur.com/olNJH.png) 

You'll never forget whether String.prototype.slice takes (start, stop) or (start, length) again!

## Section 2.3: Tooling

TypeScript allows editors to perform automated refactors which are aware of the rules of the languages.

![example](https://i.stack.imgur.com/N1C0T.gif)

Here, for instance, Visual Studio Code is able to rename references to the inner foo without altering the outer foo. This would be difficult to do with a simple find/replace.

__________

# TypeScript Core Types

## Section 3.1: String Literal Types

String literal types allow you to specify the exact value a string can have.

```ts
let myFavoritePet: "dog";
myFavoritePet = "dog";
```

Any other string will give an error.

```ts
// Error: Type '"rock"' is not assignable to type '"dog"'.
// myFavoritePet = "rock";
```

Together with Type Aliases and Union Types you get a enum-like behavior.

```
type Species = "cat" | "dog" | "bird";

function buyPet(pet: Species, name: string) : Pet { /*...*/ }

buyPet(myFavoritePet /* "dog" as defined above */, "Rocky");

// Error: Argument of type '"rock"' is not assignable to parameter of type "'cat' | "dog" | "bird".
Type '"rock"' is not assignable to type '"bird"'.
// buyPet("rock", "Rocky");
```

String Literal Types can be used to distinguish overloads.

```ts
function buyPet(pet: Species, name: string) : Pet;
function buyPet(pet: "cat", name: string): Cat;
function buyPet(pet: "dog", name: string): Dog;
function buyPet(pet: "bird", name: string): Bird;
function buyPet(pet: Species, name: string) : Pet { /*...*/ }

let dog = buyPet(myFavoritePet /* "dog" as defined above */, "Rocky");
// dog is from type Dog (dog: Dog)
```

They works well for User-Defined Type Guards.

```ts
interface Pet {
    species: Species;
    eat();
    sleep();
}
interface Cat extends Pet {
    species: "cat";
}
interface Bird extends Pet {
    species: "bird";
    sing();
}
function petIsCat(pet: Pet): pet is Cat {
    return pet.species === "cat";
}
function petIsBird(pet: Pet): pet is Bird {
    return pet.species === "bird";
}
function playWithPet(pet: Pet){
    if(petIsCat(pet)) {
        // pet is now from type Cat (pet: Cat)
        pet.eat();
        pet.sleep();
    } else if(petIsBird(pet)) {
        // pet is now from type Bird (pet: Bird)
        pet.eat();
        pet.sing();
        pet.sleep();
    }
}
```

Full Example Code

```ts
let myFavoritePet: "dog";
myFavoritePet = "dog";

// Error: Type '"rock"' is not assignable to type '"dog"'.
// myFavoritePet = "rock";

type Species = "cat" | "dog" | "bird";

interface Pet {
    species: Species;
    name: string;
    eat();
    walk();
    sleep();
}

interface Cat extends Pet {
    species: "cat";
}

interface Dog extends Pet {
    species: "dog";
}

interface Bird extends Pet {
    species: "bird";
    sing();
}

// Error: Interface 'Rock' incorrectly extends interface 'Pet'. Types of property 'species' are
incompatible. Type '"rock"' is not assignable to type '"cat" | "dog" | "bird"'. Type '"rock"' is not
assignable to type '"bird"'.
// interface Rock extends Pet {
//      type: "rock";
// }


function buyPet(pet: Species, name: string) : Pet;
function buyPet(pet: "cat", name: string): Cat;
function buyPet(pet: "dog", name: string): Dog;
function buyPet(pet: "bird", name: string): Bird;
function buyPet(pet: Species, name: string) : Pet {
    if(pet === "cat") {
        return {
            species: "cat",
            name: name,
            eat: function () {
                console.log(`${this.name} eats.`);
            },
            walk: function () {
                console.log(`${this.name} walks.`);
            },
            sleep: function () {
                console.log(`${this.name} sleeps.`);
            }
        } as Cat;
    } else if(pet === "dog") {
        return {
            species: "dog",
            name: name,
            eat: function () {
                console.log(`${this.name} eats.`);
            },
            walk: function () {
                console.log(`${this.name} walks.`);
            },
            sleep: function () {
                console.log(`${this.name} sleeps.`);
            }
        } as Dog;
    } else if(pet === "bird") {
        return {
            species: "bird",
            name: name,
            eat: function () {
                console.log(`${this.name} eats.`);
            },
            walk: function () {
                console.log(`${this.name} walks.`);
            },
            sleep: function () {
                console.log(`${this.name} sleeps.`);
            },
            sing: function () {
                console.log(`${this.name} sings.`);
            }
        } as Bird; }
    else {
        throw `Sorry we do not have a ${pet}. Would you like to buy a dog?`;
    }
}
function petIsCat(pet: Pet): pet is Cat {
    return pet.species === "cat";
}
function petIsDog(pet: Pet): pet is Dog {
    return pet.species === "dog";
}
function petIsBird(pet: Pet): pet is Bird {
    return pet.species === "bird";
}
function playWithPet(pet: Pet) {
    console.log(`Hey ${pet.name}, lets play.`);
    if(petIsCat(pet)) {
        // pet is now from type Cat (pet: Cat)
        
        pet.eat();
        pet.sleep();

        // Error: Type '"bird"' is not assignable to type '"cat"'.
        // pet.type = "bird";

        // Error: Property 'sing' does not exist on type 'Cat'.
        // pet.sing();

} else if(petIsDog(pet)) {
        // pet is now from type Dog (pet: Dog)

        pet.eat();
        pet.walk();
        pet.sleep();

} else if(petIsBird(pet)) {
        // pet is now from type Bird (pet: Bird)

        pet.eat();
        pet.sing();
        pet.sleep();
} else {
        throw "An unknown pet. Did you buy a rock?";
    }
}

let dog = buyPet(myFavoritePet /* "dog" as defined above */, "Rocky");
// dog is from type Dog (dog: Dog)

// Error: Argument of type '"rock"' is not assignable to parameter of type "'cat' | "dog" | "bird".
Type '"rock"' is not assignable to type '"bird"'.
// buyPet("rock", "Rocky");

playWithPet(dog);
// Output: Hey Rocky, lets play.
//         Rocky eats.
//         Rocky walks.
//         Rocky sleeps.

```

## Section 3.2: Tuple

Array type with known and possibly different types:

```ts
let day: [number, string];
day = [0, 'Monday']; // valid
day = ['zero', 'Monday']; // invalid: 'zero' is not numeric console.log(day[0]); // 0
console.log(day[1]); // Monday

day[2] = 'Saturday'; // valid: [0, 'Saturday']
day[3] = false; // invalid: must be union type of 'number | string'
```

## Section 3.3: Boolean

A boolean represents the most basic datatype in TypeScript, with the purpose of assigning true/false values.

```ts
// set with initial value (either true or false)
let isTrue: boolean = true;

// defaults to 'undefined', when not explicitly set
let unsetBool: boolean;

// can also be set to 'null' as well
let nullableBool: boolean = null;
```

## Section 3.4: Intersection Types

A Intersection Type combines the member of two or more types.

```
interface Knife {
    cut();
}
interface BottleOpener{
    openBottle();
}
interface Screwdriver{
    turnScrew();
}
type SwissArmyKnife = Knife & BottleOpener & Screwdriver;

function use(tool: SwissArmyKnife){
    console.log("I can do anything!");
    tool.cut();
    tool.openBottle();
    tool.turnScrew();
}
```

## Section 3.5: Types in function arguments and return value. Number

When you create a function in TypeScript you can specify the data type of the function's arguments and the data type for the return value

Example:

```ts
function sum(x: number, y: number): number {
    return x + y;
}
```

Here the syntax x: number, y: number means that the function can accept two argumentsx and y and they can only be numbers and (...): number { means that the return value can only be a number

Usage:

```ts
sum(84 + 76) // will be return 160
```

Note:

You can not do so

```ts
function sum(x: string, y: string): number {
    return x + y;
}
```
or

```ts
function sum(x: number, y: number): string {
    return x + y;
}
```

it will receive the following errors:

error TS2322: Type 'string' is not assignable to type 'number' and error TS2322: Type 'number' is
not assignable to type 'string' respectively

## Section 3.6: Types in function arguments and return value. String

Example:

```ts
function hello(name: string): string {
    return `Hello ${name}!`;
}
```

Here the syntax name: string means that the function can accept one name argument and this argument can only be string and (...): string { means that the return value can only be a string

Usage:

```ts
hello('StackOverflow Documentation') // will be return Hello StackOverflow Documentation!
```

## Section 3.7: const Enum

A const Enum is the same as a normal Enum. Except that no Object is generated at compile time. Instead, the literal values are substituted where the const Enum is used.

```ts
// TypeScript: A const Enum can be defined like a normal Enum (with start value, specific values, etc.)

const enum NinjaActivity {
    Espionage,
    Sabotage,
    Assassination
}

// JavaScript: But nothing is generated

// TypeScript: Except if you use it
let myFavoriteNinjaActivity = NinjaActivity.Espionage;
console.log(myFavoritePirateActivity); // 0

// JavaScript: Then only the number of the value is compiled into the code
// var myFavoriteNinjaActivity = 0 /* Espionage */;
// console.log(myFavoritePirateActivity); // 0

// TypeScript: The same for the other constant example
console.log(NinjaActivity["Sabotage"]); // 1

// JavaScript: Just the number and in a comment the name of the value
// console.log(1 /* "Sabotage" */); // 1

// TypeScript: But without the object none runtime access is possible
// Error: A const enum member can only be accessed using a string literal.
// console.log(NinjaActivity[myFavoriteNinjaActivity]);

```

For comparison, a normal Enum

```ts
// TypeScript: A normal Enum
enum PirateActivity {
    Boarding,
    Drinking,
    Fencing
}

// JavaScript: The Enum after the compiling
// var PirateActivity;
// (function (PirateActivity) {
//     PirateActivity[PirateActivity["Boarding"] = 0] = "Boarding";
//     PirateActivity[PirateActivity["Drinking"] = 1] = "Drinking";
//     PirateActivity[PirateActivity["Fencing"] = 2] = "Fencing";
// })(PirateActivity || (PirateActivity = {}));

// TypeScript: A normal use of this Enum
let myFavoritePirateActivity = PirateActivity.Boarding;
console.log(myFavoritePirateActivity); // 0

// JavaScript: Looks quite similar in JavaScript
// let myFavoritePirateActivity = PirateActivity.Boarding;
// console.log(myFavoritePirateActivity); // 0

// TypeScript: And some other normal use
console.log(PirateActivity["Drinking"]); // 1

// JavaScript: Looks quite similar in JavaScript
// console.log(PirateActivity["Drinking"]); // 1

// TypeScript: At runtime, you can access an normal enum
console.log(PirateActivity[myFavoritePirateActivity]); // "Boarding"

// JavaScript: And it will be resolved at runtime
// console.log(PirateActivity[myFavoritePirateActivity]); // "Boarding"
```

## Section 3.8: Number

Like JavaScript, numbers are floating point values.

```ts
let pi: number = 3.14; // base 10 decimal by default
let hexadecimal: number = 0xFF; // 255 in decimal
```

ECMAScript 2015 allows binary and octal.

```ts
let binary: number = 0b10; // 2 in decimal
let octal: number = 0o755; // 493 in decimal
```

Section 3.9: String

Textual data type:

```ts
let singleQuotes: string = 'single';
let doubleQuotes: string = "double";
let templateString: string = `I am ${ singleQuotes }`; // I am single
```

## Section 3.10: Array

An array of values:

```ts
let threePigs: number[] = [1, 2, 3];
let genericStringArray: Array<string> = ['first', '2nd', '3rd'];
```

## Section 3.11: Enum

A type to name a set of numeric values: 

Number values default to 0:

```ts
enum Day { Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday };
let bestDay: Day = Day.Saturday;
```

Set a default starting number:

```ts
enum TenPlus { Ten = 10, Eleven, Twelve }
```

or assign values:

```ts
enum MyOddSet { Three = 3, Five = 5, Seven = 7, Nine = 9 }
```

## Section 3.12: Any

When unsure of a type, any is available:

```ts
let anything: any = 'I am a string';
anything = 5; // but now I am the number 5
```

## Section 3.13: Void

If you have no type at all, commonly used for functions that do not return anything:

```ts
function log(): void {
    console.log('I return nothing');
}
```

void types Can only be assigned null or undefined.

------------------

# Arrays

## Section 4.1: Finding Object in Array

### Using find()

```ts
const inventory = [
        {name: 'apples', quantity: 2},
        {name: 'bananas', quantity: 0},
        {name: 'cherries', quantity: 5}
];

function findCherries(fruit) {
        return fruit.name === 'cherries';
}

inventory.find(findCherries); // { name: 'cherries', quantity: 5 }

/* OR */

inventory.find(e => e.name === 'apples'); // { name: 'apples', quantity: 2 }
```

-----------------------------

# Enums

## Enums with explicit values

By default all enum values are resolved to numbers. Let's say if you have something like

```ts
enum MimeType {
    JPEG,
    PNG,
    PDF
}
```

the real value behind e.g. MimeType.PDF will be 2.

But some of the time it is important to have the enum resolve to a different type. E.g. you receive the value from backend / frontend / another system which is definitely a string. This could be a pain, but luckily there is this method:

```ts
enum MimeType {
  JPEG = <any>'image/jpeg',
  PNG = <any>'image/png',
  PDF = <any>'application/pdf'
}
```

This resolves the MimeType.PDF to application/pdf. 

Since TypeScript 2.4 it's possible to declare string enums:

```ts
enum MimeType {
  JPEG = 'image/jpeg',
  PNG = 'image/png',
  PDF = 'application/pdf',
}
```

You can explicitly provide numeric values using the same method

```ts
enum MyType {
    Value = 3,
    ValueEx = 30,
    ValueEx2 = 300
}
```

Fancier types also work, since non-const enums are real objects at runtime, for example


```ts
enum FancyType {
   OneArr = <any>[1],
   TwoArr = <any>[2, 2],
   ThreeArr = <any>[3, 3, 3]
}
```

becomes

```ts
let FancyType;
(function (FancyType) {
    FancyType[FancyType["OneArr"] = [1]] = "OneArr";
    FancyType[FancyType["TwoArr"] = [2, 2]] = "TwoArr";
    FancyType[FancyType["ThreeArr"] = [3, 3, 3]] = "ThreeArr";
})(FancyType || (FancyType = {}));
```

## Section 5.2: How to get all enum values

```ts
enum SomeEnum { A, B }
let enumValues:Array<string>= [];
for(let value in SomeEnum) {
if(typeof SomeEnum[value] === 'number') {
        enumValues.push(value);
    }
}
enumValues.forEach(v=> console.log(v))
//A
//B
```

## Section 5.3: Extending enums without custom enum implementation

```ts
enum SourceEnum {
  value1 = <any>'value1',
  value2 = <any>'value2'
}

enum AdditionToSourceEnum {
  value3 = <any>'value3',
  value4 = <any>'value4'
}

// we need this type for TypeScript to resolve the types correctly
type TestEnumType = SourceEnum | AdditionToSourceEnum;
// and we need this value "instance" to use values
let TestEnum = Object.assign({}, SourceEnum, AdditionToSourceEnum); // also works fine the TypeScript 2 feature
// let TestEnum = { ...SourceEnum, ...AdditionToSourceEnum };

function check(test: TestEnumType) {
    return test === TestEnum.value2;
}
console.log(TestEnum.value1);
console.log(TestEnum.value2 === <any>'value2');
console.log(check(TestEnum.value2));
console.log(check(TestEnum.value3));
```

## Section 5.4: Custom enum implementation: extends for enums

Sometimes it is required to implement Enum on your own. E.g. there is no clear way to extend other enums. Custom implementation allows this:

```ts
class Enum {
  constructor(protected value: string) {}

  public toString() {
        return String(this.value);
    }

    public is(value: Enum | string) {
        return this.value = value.toString();
    }
}

class SourceEnum extends Enum {
    public static value1 = new SourceEnum('value1');
    public static value2 = new SourceEnum('value2');
}

class TestEnum extends SourceEnum {
    public static value3 = new TestEnum('value3');
    public static value4 = new TestEnum('value4');
}

function check(test: TestEnum) {
    return test === TestEnum.value2;
}

let value1 = TestEnum.value1;

console.log(value1 + 'hello');
console.log(value1.toString() === 'value1');
console.log(value1.is('value1'));
console.log(!TestEnum.value3.is(TestEnum.value3));
console.log(check(TestEnum.value2));
// this works but perhaps your TSLint would complain // attention! does not work with ===
// use .is() instead
console.log(TestEnum.value1 == <any>'value1');
```

------------------------------------

