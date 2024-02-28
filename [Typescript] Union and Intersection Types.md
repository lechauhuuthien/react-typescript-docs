## Union Types: The Power of "Or"

Union types, represented by the pipe symbol (|), allow a variable, parameter, or return value to hold one of several possible data types. Think of them as an "or" relationship between types.

### Practical Example 1: Flexible Functions

```typeScript
function getLength(value: number | string): number {
  if (typeof value === "string") {
    return value.length;  // String has a .length property
  } else {
    return value.toString().length;  // Convert number to string first
  }
}

console.log(getLength(100)); // Output: 3
console.log(getLength("hello world")); // Output: 11
```

### Practical Example 2: Multiple Event Handlers

```typeScript
type MouseEvent = { clientX: number, clientY: number };
type KeyboardEvent = { keyCode: number };

function handleEvent(event: MouseEvent | KeyboardEvent) {
  if ('clientX' in event) {
    // Handle MouseEvent
  } else {
    // Handle KeyboardEvent
  }
}
```

## Intersection Types: The Power of "And"

Intersection Types, represented by the ampersand symbol (&), combine multiple types into a single type that must have all the properties from the combined types. Think of them as an "and" relationship.

### Practical Example 1: Combining Features

```typeScript
interface Employee {
  name: string;
  id: number;
}

interface Project {
  name: string;
  budget: number;
}

type ProjectManager = Employee & Project;  // Has properties from both types

const manager: ProjectManager = {
  name: "John Doe",
  id: 123,
  project: "Development",
  budget: 100000
};
```

### Practical Example 2: Mixins

```typeScript
interface HasName { 
  name: string; 
}

interface HasAge { 
  age: number; 
}

type Person = HasName & HasAge; 
```

## Tips

- `Choose wisely:` Union types for "either/or" scenarios; Intersection types for "this and that" scenarios.
- `Narrowing types:` Use type guards (e.g., typeof checks, in operator) to discriminate unions for fine-grained control.
- `Combine with generics:` Create flexible functions and components that operate on types defined by unions and intersections.
Example: Combining Intersection and Union

```typeScript
interface Error { message: string; }
interface Loading { isLoading: boolean; }

type ResponseState = (Error | Loading) & { data?: any };
```