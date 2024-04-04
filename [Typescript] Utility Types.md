Utility types in TypeScript are pre-defined generic types that provide convenient ways to manipulate existing types. Let's go through several utility types along with practical examples for each:

### 1. `Partial<T>`
The `Partial<T>` utility type constructs a type with all properties of `T` set to optional.

**Example:**
```typescript
interface Student {
    name: string;
    age: number;
    grade: string;
}

function updateStudent(student: Partial<Student>, newData: Partial<Student>): Student {
    return { ...student, ...newData };
}

const student: Student = { name: "Alice", age: 20, grade: "A" };
const updatedStudent = updateStudent(student, { age: 21 });
console.log(updatedStudent); // Output: { name: 'Alice', age: 21, grade: 'A' }
```

### 2. `Required<T>`
The `Required<T>` utility type constructs a type with all properties of `T` set to required.

**Example:**
```typescript
interface PartialStudent {
    name?: string;
    age?: number;
    grade?: string;
}

type RequiredStudent = Required<PartialStudent>;

const requiredStudent: RequiredStudent = { name: "Bob", age: 22, grade: "B" }; // All properties are required
```

### 3. `Readonly<T>`
The `Readonly<T>` utility type constructs a type with all properties of `T` set to readonly.

**Example:**
```typescript
interface Student {
    name: string;
    age: number;
    grade: string;
}

const readOnlyStudent: Readonly<Student> = { name: "Charlie", age: 19, grade: "C" };
// readOnlyStudent.age = 20; // Error: Cannot assign to 'age' because it is a read-only property.
```

### 4. `Record<K, T>`
The `Record<K, T>` utility type constructs an object type with properties `K` of type `T`.

**Example:**
```typescript
type Subjects = 'Math' | 'Science' | 'History';
type GradeRecord = Record<Subjects, number>;

const grades: GradeRecord = { Math: 90, Science: 85, History: 80 };
```

### 5. `Pick<T, K>`
The `Pick<T, K>` utility type constructs a type by picking the set of properties `K` from `T`.

**Example:**
```typescript
interface Student {
    name: string;
    age: number;
    grade: string;
    address: string;
}

type StudentInfo = Pick<Student, 'name' | 'age'>;

const studentInfo: StudentInfo = { name: "David", age: 18 }; // Only 'name' and 'age' properties are picked
```

### 6. `Omit<T, K>`
The `Omit<T, K>` utility type constructs a type by excluding the set of properties `K` from `T`.

**Example:**
```typescript
interface Student {
    name: string;
    age: number;
    grade: string;
    address: string;
}

type StudentDetails = Omit<Student, 'name' | 'age'>;

const studentDetails: StudentDetails = { grade: "A", address: "123 Main St" }; // Excludes 'name' and 'age' properties
```