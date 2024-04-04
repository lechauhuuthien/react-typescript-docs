# Generics
Generic types in TypeScript allow you to create reusable components that can work with a variety of data types while maintaining type safety. They provide flexibility by allowing types to be parameterized, enabling the creation of functions, classes, and interfaces that can work with any data type. Let's explore their features and provide practical examples:

### Features:

1. **Type Parameterization**: Generics allow you to define types with one or more type parameters, which can be used within the type definition.
2. **Type Inference**: TypeScript infers types based on usage when generics are used, reducing the need for explicit type annotations.
3. **Type Safety**: Generics ensure type safety by preserving type information at compile-time, preventing type errors.

### Practical Examples:

#### 1. Generic Function:
```typescript
function identity<T>(arg: T): T {
    return arg;
}

// Usage
const result1 = identity<string>("Hello"); // Type of result1: string
const result2 = identity<number>(42); // Type of result2: number
```
In this example, the `identity` function is generic, allowing it to work with any type `T`. It returns the same type as the input argument.

#### 2. Generic Class:
```typescript
class Box<T> {
    private value: T;

    constructor(value: T) {
        this.value = value;
    }

    getValue(): T {
        return this.value;
    }
}

// Usage
const box1 = new Box<string>("Hello");
console.log(box1.getValue()); // Output: Hello

const box2 = new Box<number>(42);
console.log(box2.getValue()); // Output: 42
```
Here, the `Box` class is generic, allowing it to hold values of any type `T`.

#### 3. Generic Interface:
```typescript
interface Pair<T, U> {
    first: T;
    second: U;
}

// Usage
const pair: Pair<string, number> = { first: "one", second: 1 };
```
This example defines a generic interface `Pair`, which represents a pair of values of types `T` and `U`.

#### 4. Generic Constraints:
```typescript
interface Comparable {
    compareTo(other: this): number;
}

function max<T extends Comparable>(a: T, b: T): T {
    return a.compareTo(b) > 0 ? a : b;
}

// Usage
class NumberWrapper implements Comparable {
    constructor(private value: number) {}

    compareTo(other: NumberWrapper): number {
        return this.value - other.value;
    }
}

const result = max(new NumberWrapper(5), new NumberWrapper(10)); // Result: NumberWrapper with value 10
```
In this example, the `max` function has a generic constraint `T extends Comparable`, ensuring that `T` is a type that implements the `Comparable` interface.

#### 5. Generic Utility Functions:
```typescript
function toArray<T>(value: T): T[] {
    return [value];
}

// Usage
const array1 = toArray("Hello"); // Type of array1: string[]
const array2 = toArray(42); // Type of array2: number[]
```
Here, the `toArray` function is generic, converting a value of type `T` into an array of type `T[]`.

# Keyof
The `keyof` type operator in TypeScript retrieves the union type of all property names of a given type. It's particularly useful for scenarios where you need to work with property names dynamically or create new types based on existing ones. Let's explore its features and practical examples:

### Features:

1. **Property Name Extraction**: `keyof` allows you to extract property names from a type, creating a union of those names.
2. **Type Safety**: Since TypeScript is statically typed, `keyof` ensures that only existing property names are included in the resulting union type.
3. **Dynamic Access**: It enables dynamic access to object properties and helps in writing generic code that works with various types.

### Practical Examples:

#### 1. Basic Usage:
```typescript
interface Student {
    name: string;
    age: number;
    grade: string;
}

type StudentKeys = keyof Student; // Result: 'name' | 'age' | 'grade'
```
In this example, `keyof Student` retrieves a union type containing the names of all properties in the `Student` interface.

#### 2. Dynamic Property Access:
```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
    return obj[key];
}

const student: Student = { name: "Alice", age: 20, grade: "A" };
const name: string = getProperty(student, 'name'); // Accessing property dynamically
```
This function `getProperty` accepts an object `obj` of type `T` and a property key `key` of type `K`, where `K` extends `keyof T`. It retrieves the value of the specified property from the object dynamically.

#### 3. Creating Mapped Types:
```typescript
type StudentProps = {
    [K in keyof Student]: K;
}

// Result: { name: 'name', age: 'age', grade: 'grade' }
```
Here, `StudentProps` is a mapped type that transforms each property in `Student` into a property with the same name but with a string literal type representing the original property name.

#### 4. Dynamic Property Assignment:
```typescript
function updateProperty<T, K extends keyof T>(obj: T, key: K, value: T[K]): void {
    obj[key] = value;
}

const student: Student = { name: "Bob", age: 21, grade: "B" };
updateProperty(student, 'age', 22); // Dynamically update property 'age'
```
This function `updateProperty` allows dynamically assigning values to object properties based on the provided key.

#### 5. Type Constraints:
```typescript
function printProperty<T, K extends keyof T>(obj: T, key: K): void {
    console.log(obj[key]);
}

const student: Student = { name: "Charlie", age: 19, grade: "C" };
printProperty(student, 'name'); // Accessing and printing property 'name'
```
In this example, the function `printProperty` enforces a constraint such that the `key` parameter must be a valid property name of the type `T`.
# Typeof
The `typeof` type operator in TypeScript is used to obtain the type of a variable or an expression at compile-time. It's similar to the `typeof` operator in JavaScript but operates at the type level rather than the runtime level. Let's explore its features and provide practical examples:

### Features:

1. **Compile-time Type Retrieval**: `typeof` allows you to retrieve the type of a variable or an expression during the compilation process.
2. **Type Safety**: Since TypeScript is statically typed, `typeof` ensures that the retrieved type matches the actual type of the variable or expression.
3. **Type Inference**: It can be used in type inference scenarios, where TypeScript infers types based on their usage.

### Practical Examples:

#### 1. Obtaining Type of a Variable:
```typescript
const num = 42;
type NumType = typeof num; // Result: number
```
In this example, `typeof num` retrieves the type of the variable `num`, which is inferred to be `number`.

#### 2. Creating Type Aliases:
```typescript
const person = {
    name: "Alice",
    age: 30,
};

type Person = typeof person; // Result: { name: string, age: number }
```
Here, `typeof person` retrieves the type of the object `person`, and we create a type alias `Person` based on that type.

#### 3. Type Guards:
```typescript
function processValue(value: string | number) {
    if (typeof value === 'string') {
        // value is treated as a string here
    } else {
        // value is treated as a number here
    }
}
```
The `typeof` operator can be used in type guards to differentiate between different types of values at runtime.

#### 4. Ensuring Consistency:
```typescript
const defaultValue = 42;
let value: typeof defaultValue;
value = 50; // Error: Type '50' is not assignable to type 'typeof defaultValue'
```
In this case, `value` is inferred to have the same type as `defaultValue`, ensuring consistency in the assignment.

#### 5. Dynamic Object Properties:
```typescript
const config = {
    debug: true,
    port: 3000,
};

type ConfigKeys = keyof typeof config; // Result: 'debug' | 'port'
```
Here, `typeof config` retrieves the type of the `config` object, and we use `keyof` to obtain a union type of its keys.

#### 6. Inferring Generic Types:
```typescript
function identity<T>(arg: T): T {
    return arg;
}

const result = identity(42);
type ResultType = typeof result; // Result: number
```
In this example, the type of `result` is inferred based on the return type of the `identity` function, leveraging `typeof`.
# Indexed Access
Indexed Access Types, often used in TypeScript, allow you to dynamically access the type of a property within another type. They provide a way to index into a type using another type, allowing for more flexible and dynamic type definitions. Let's delve into its features and offer practical examples:

### Features:

1. **Dynamic Typing**: Indexed Access Types enable accessing the type of a property using a dynamic key or set of keys.
2. **Type Safety**: TypeScript ensures that indexed access is done on existing properties, offering type safety at compile time.
3. **Generics Compatibility**: Indexed Access Types work seamlessly with generics, providing flexible and reusable type definitions.

### Practical Examples:

#### 1. Basic Indexed Access:
```typescript
interface Student {
    name: string;
    age: number;
    grade: string;
}

type StudentName = Student['name']; // Result: string
```
Here, `Student['name']` accesses the type of the `name` property within the `Student` interface, resulting in the type `string`.

#### 2. Accessing Union Types:
```typescript
interface Options {
    method: 'GET' | 'POST';
    headers: { [key: string]: string };
}

type HeaderValue = Options['headers']['Content-Type']; // Result: string
```
In this example, we access the type of the `Content-Type` header within the `headers` property of the `Options` interface.

#### 3. Using Indexed Access with Generics:
```typescript
interface Dictionary<T> {
    [key: string]: T;
}

type NumberDictionary = Dictionary<number>; // Result: { [key: string]: number; }
```
Here, `Dictionary<T>` defines a generic dictionary type, and `Dictionary<number>` accesses the type of a dictionary with string keys and number values.

#### 4. Nested Indexed Access:
```typescript
interface User {
    id: number;
    info: {
        name: string;
        email: string;
    };
}

type UserName = User['info']['name']; // Result: string
```
This example demonstrates nested indexed access, where we access the type of the `name` property within the `info` property of the `User` interface.

#### 5. Combining with Conditional Types:
```typescript
interface Product {
    id: number;
    name: string;
    price: number;
}

type NumericKeys<T> = {
    [K in keyof T]: T[K] extends number ? K : never;
}[keyof T];

type ProductNumericKeys = NumericKeys<Product>; // Result: 'id' | 'price'
```
Here, we define a conditional type `NumericKeys<T>` to extract keys from the `Product` interface that have a numeric value type.

# Conditional
Conditional types in TypeScript allow you to create types that depend on the evaluation of a condition. They enable you to define types based on the properties or types of other types. Let's explore their features and provide practical examples:

### Features:

1. **Type Dependency**: Conditional types enable the definition of types that depend on the evaluation of conditions.
2. **Type Inference**: They allow TypeScript to infer types based on conditions, providing flexibility in type definitions.
3. **Type Transformation**: Conditional types can transform one type into another based on specified conditions, enhancing type safety.

### Practical Examples:

#### 1. Basic Conditional Type:
```typescript
type Check<T> = T extends string ? true : false;

type IsString = Check<string>; // Result: true
type IsNumber = Check<number>; // Result: false
```
Here, `Check<T>` is a conditional type that evaluates whether `T` extends `string`. If true, it returns `true`; otherwise, it returns `false`.

#### 2. Conditional Type with Union:
```typescript
type TypeName<T> = 
    T extends string ? "string" :
    T extends number ? "number" :
    "other";

type StringTypeName = TypeName<string>; // Result: "string"
type NumberTypeName = TypeName<number>; // Result: "number"
type OtherTypeName = TypeName<boolean>; // Result: "other"
```
In this example, `TypeName<T>` checks the type of `T` and returns a string literal type based on the type of `T`.

#### 3. Filtering Types with Conditional Type:
```typescript
type Filter<T> = {
    [K in keyof T]: T[K] extends number ? K : never;
};

interface Product {
    id: number;
    name: string;
    price: number;
}

type NumericKeys = Filter<Product>; // Result: { id: number; price: number; }
```
Here, `Filter<T>` creates a new type containing only properties of `T` that have a numeric value.

#### 4. Optional Properties with Conditional Type:
```typescript
type OptionalProperties<T> = {
    [K in keyof T]?: T[K];
};

interface Car {
    brand: string;
    model: string;
    year: number;
}

type OptionalCar = OptionalProperties<Car>;
```
In this example, `OptionalProperties<T>` creates a new type where all properties of `T` are optional.

#### 5. Conditional Type with Union of Object Types:
```typescript
type Shape = Circle | Square;

interface Circle {
    kind: 'circle';
    radius: number;
}

interface Square {
    kind: 'square';
    sideLength: number;
}

type GetArea<T extends Shape> = T extends { kind: 'circle' } ? Math.PI * T['radius'] ** 2 : T['sideLength'] ** 2;

const circle: Circle = { kind: 'circle', radius: 5 };
const square: Square = { kind: 'square', sideLength: 4 };

const circleArea: number = GetArea(circle); // Result: 78.54
const squareArea: number = GetArea(square); // Result: 16
```
In this example, `GetArea<T>` is a conditional type that calculates the area based on the type of the shape (`Circle` or `Square`).

Conditional types in TypeScript offer a powerful mechanism for defining types based on conditions, making them valuable tools for building flexible and type-safe code.
# Mapped
Mapped types in TypeScript allow you to create new types based on existing ones by iterating over the properties of the existing type and applying transformations to them. They provide a concise way to define new types that are variations of existing ones. Let's explore their features and provide practical examples:

### Features:

1. **Property Transformation**: Mapped types enable the transformation of properties in an existing type according to a specified mapping function.
2. **Dynamic Typing**: They allow for the creation of types dynamically based on the properties of other types.
3. **Type Safety**: Mapped types ensure that the resulting types maintain type safety, even after transformation.

### Practical Examples:

#### 1. Making All Properties Readonly:
```typescript
interface MutablePerson {
    name: string;
    age: number;
}

type ReadonlyPerson = {
    readonly [K in keyof MutablePerson]: MutablePerson[K];
};

const person: ReadonlyPerson = { name: "Alice", age: 30 };
// person.name = "Bob"; // Error: Cannot assign to 'name' because it is a read-only property.
```
In this example, `ReadonlyPerson` is a mapped type that makes all properties of `MutablePerson` readonly.

#### 2. Making All Properties Optional:
```typescript
interface RequiredFields {
    name: string;
    age: number;
}

type OptionalFields<T> = {
    [K in keyof T]?: T[K];
};

type PartialPerson = OptionalFields<RequiredFields>;

const partialPerson: PartialPerson = { name: "Bob" };
```
Here, `OptionalFields<T>` is a mapped type that makes all properties of `T` optional, creating a type `PartialPerson` with optional properties.

#### 3. Making All Properties Nullable:
```typescript
interface NonNullableFields {
    name: string;
    age: number;
}

type NullableFields<T> = {
    [K in keyof T]: T[K] | null;
};

type NullablePerson = NullableFields<NonNullableFields>;

const nullablePerson: NullablePerson = { name: null, age: null };
```
This example defines `NullableFields<T>`, a mapped type that makes all properties of `T` nullable, creating a type `NullablePerson` with nullable properties.

#### 4. Adding Prefix to Property Names:
```typescript
interface Person {
    name: string;
    age: number;
}

type PrefixedPerson = {
    [K in keyof Person as `prefixed_${K}`]: Person[K];
};

const prefixedPerson: PrefixedPerson = { prefixed_name: "Alice", prefixed_age: 30 };
```
In this example, `PrefixedPerson` is a mapped type that adds a prefix `prefixed_` to all property names of `Person`.

#### 5. Creating Union Types:
```typescript
type Fruit = "apple" | "banana" | "orange";

type FruitWithPrice = {
    [K in Fruit]: number;
};

const fruitPrices: FruitWithPrice = { apple: 1.5, banana: 2, orange: 1 };
```
Here, `FruitWithPrice` is a mapped type that creates a union type of fruit names (`Fruit`) and assigns each a number type representing its price.

# Template Literal
Template literal types, introduced in TypeScript 4.1, are string literal types that enable the creation of string types based on template literal patterns. They allow you to specify precise string shapes by combining string literals with placeholders for variables or expressions. Let's delve into their features and provide practical examples:

### Features:

1. **String Shape Specification**: Template literal types allow you to define specific string patterns based on literals and placeholders.
2. **Type Safety**: They provide type safety by ensuring that values conform to the specified string shape.
3. **Flexible Typing**: Template literal types support a wide range of patterns, including concatenation, interpolation, and multiline strings.

### Practical Examples:

#### 1. Basic Template Literal Type:
```typescript
type Greeting = `Hello, ${string}!`;

const greeting: Greeting = "Hello, Alice!";
// const greeting: Greeting = "Hi, Bob!"; // Error: Type '"Hi, Bob!"' is not assignable to type 'Greeting'.
```
In this example, `Greeting` is a template literal type that matches strings starting with "Hello, " and ending with "!", with a variable string in between.

#### 2. Numeric Sequence Pattern:
```typescript
type NumberSequence = `${number}-${number}-${number}`;

const sequence: NumberSequence = "1-2-3";
// const sequence: NumberSequence = "1-2-3-4"; // Error: Type '"1-2-3-4"' is not assignable to type 'NumberSequence'.
```
Here, `NumberSequence` is a template literal type representing strings of the format "x-y-z", where x, y, and z are numbers.

#### 3. Email Address Pattern:
```typescript
type EmailAddress = `${string}@${string}.${string}`;

const email: EmailAddress = "alice@example.com";
// const email: EmailAddress = "invalid-email"; // Error: Type '"invalid-email"' is not assignable to type 'EmailAddress'.
```
This example defines `EmailAddress` as a template literal type matching typical email address patterns.

#### 4. Dynamic Typing:
```typescript
type DynamicPath<T extends string> = `/${T}/${string}`;

const profilePath: DynamicPath<"profile"> = "/profile/username";
const postPath: DynamicPath<"posts"> = "/posts/postId";
```
Here, `DynamicPath` is a generic template literal type that matches paths starting with a specified segment, followed by a variable string segment.

#### 5. Multiline String Pattern:
```typescript
type MultilineString = `
    Line 1
    Line 2
    Line 3
`;

const text: MultilineString = `
    Line 1
    Line 2
    Line 3
`;
```
Template literal types can represent multiline string patterns without the need for escape characters, providing improved readability and type safety.

#### 6. Complex Patterns with Conditional Types:
```typescript
type StatusMessage<S extends string> = S extends "success"
    ? `Success: ${string}`
    : S extends "error"
    ? `Error: ${string}`
    : never;

const successMessage: StatusMessage<"success"> = "Success: Operation completed.";
const errorMessage: StatusMessage<"error"> = "Error: Operation failed.";
```
In this example, `StatusMessage` is a conditional template literal type that matches different status message patterns based on the input string.