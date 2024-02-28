## TypeScript Basics

### Syntax and Data Types:
- `Syntax:` TypeScript syntax closely resembles JavaScript. You can declare variables using let or const, define functions with function or arrow syntax () => {}, use conditional statements (if, else, switch), loops (for, while), and other constructs.


```typescript
let num: number = 10;
const message: string = "Hello, TypeScript!";

function greet(name: string): void {
    console.log("Hello, " + name + "!");
}

for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

- `Data Types:` TypeScript supports the same primitive data types as JavaScript (number, string, boolean, null, undefined) along with additional types like object, any, void, never.

```typescript
let num: number = 10;
let message: string = "Hello, TypeScript!";
let isValid: boolean = true;
let nullValue: null = null;
let undefinedValue: undefined = undefined;
```

### Type Annotations and Type Inference:

- `Type Annotations:` Type annotations allow you to explicitly specify the type of a variable, function parameter, or function return type.

```typescript
let num: number = 10;
function add(x: number, y: number): number {
    return x + y;
}
```

- `Type Inference:` TypeScript can infer types based on the context. If you don't explicitly specify a type, TypeScript will infer it based on the value assigned.

```typescript
let num = 10; // TypeScript infers 'number' type for 'num'
function add(x, y) {
    return x + y; // TypeScript infers 'number' type for the return value
}
```

### Functions and Function Types:

- `Functions:` You can define functions in TypeScript using the function keyword or arrow functions (() => {}).

```typescript
function greet(name: string): void {
    console.log("Hello, " + name + "!");
}

const multiply = (x: number, y: number): number => {
    return x * y;
};
```

- `Function Types:` TypeScript allows you to define function types, which specify the signature of a function. Function types can be used to enforce type compatibility when passing functions as arguments or returning functions from other functions.

```typescript
type MathOperation = (x: number, y: number) => number;

function performOperation(operation: MathOperation, x: number, y: number): number {
    return operation(x, y);
}
```

### Arrays and Tuples:
- `Arrays:` TypeScript supports arrays, which can hold multiple values of the same type. You can specify the type of elements in an array using square brackets ([]).

```typescript
let numbers: number[] = [1, 2, 3, 4, 5];
```

- `Tuples:` Tuples allow you to express an array with a fixed number of elements, where each element may have a different type.

```typescript
let person: [string, number] = ["John", 30];
```

### Enums and Literal Types:
- `Enums:` Enums allow you to define a set of named constants. They make it easier to work with sets of related values.

```typescript
enum Color {
    Red,
    Green,
    Blue,
}

let backgroundColor: Color = Color.Blue;
```

- `Literal Types:` Literal types allow you to specify exact values that a variable can have.

```typescript
let status: "success" | "error" | "pending";
status = "success";
```


### Interfaces and Type Aliases:
- `Interfaces:` Interfaces allow you to define the shape of objects in TypeScript. They specify the properties and methods that an object must have.

```typescript
interface Person {
    name: string;
    age: number;
}

function greet(person: Person): void {
    console.log("Hello, " + person.name + "!");
}
```

- `Type Aliases:` Type aliases enable you to create custom names for types. They are useful for simplifying complex type definitions.

```typescript
type Point = {
    x: number;
    y: number;
}

function printPoint(point: Point): void {
    console.log("x: " + point.x + ", y: " + point.y);
}
```
