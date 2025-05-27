# TypeScript Generics and Interfaces Explanation

## Interfaces
An interface is a way to define a contract for an object's shape. It specifies what properties and methods an object must have.

Example of our Task interface:
```typescript
interface Task {
    text: string;      // Must have a text property of type string
    completed: boolean; // Must have a completed property of type boolean
}
```

You can use this interface to ensure objects follow this structure:
```typescript
// Valid usage
const task: Task = {
    text: "Learn Vue",
    completed: false
}

// Invalid usage - will show error
const invalidTask: Task = {
    text: "Learn Vue"
    // Error: missing 'completed' property
}
```

## Generics
Generics allow you to write flexible, reusable code that works with different types while maintaining type safety.

In our code:
```typescript
const tasks = ref<Task[]>([]);
```

This means:
- `ref<Task[]>` is a generic type
- `Task[]` is the type argument (an array of Task objects)
- The ref will only accept arrays containing objects that match the Task interface

Other generic examples:
```typescript
// Generic array
const numbers: Array<number> = [1, 2, 3];
const strings: Array<string> = ["a", "b", "c"];

// Generic function
function firstItem<T>(array: T[]): T | undefined {
    return array[0];
}

// Usage
const first = firstItem<Task>(tasks.value); // Returns a Task or undefined
```

### Why Use Generics?
1. Type Safety: Catch errors at compile time
2. Code Reusability: Write functions that work with multiple types
3. Better IDE Support: Get better autocomplete and type hints