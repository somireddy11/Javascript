# Javascript


The difference between a **shallow copy** and a **deep copy** lies in how they handle objects and their nested structures, particularly when dealing with objects that contain other objects or arrays as properties.

### 1. **Shallow Copy**

A shallow copy creates a new object or array, but only copies the references of nested objects, not the actual nested objects themselves. So, if the original object has nested objects, a shallow copy will still point to the same nested objects rather than creating independent copies. 

#### Example of a Shallow Copy

```javascript
const original = {
    name: "Alice",
    details: { age: 25, city: "New York" }
};

const shallowCopy = { ...original };
shallowCopy.details.age = 30;

console.log(original.details.age); // 30
```

In this example:
- We create a shallow copy of `original` using the spread operator `{ ...original }`.
- The top-level properties (like `name`) are copied, but `details` (a nested object) is still a reference to the same object as in `original`.
- Changing `shallowCopy.details.age` also changes `original.details.age`, because both `original.details` and `shallowCopy.details` reference the same object.

#### Common Ways to Make a Shallow Copy
- Using the **spread operator**: `{ ...object }`
- Using **Object.assign**: `Object.assign({}, object)`
- Using **Array.slice** or **Array.from** for arrays

### 2. **Deep Copy**

A deep copy creates a new object or array, along with independent copies of all nested objects and arrays. Any changes made to nested objects in the copied object will not affect the original object and vice versa.

#### Example of a Deep Copy

```javascript
const original = {
    name: "Alice",
    details: { age: 25, city: "New York" }
};

const deepCopy = JSON.parse(JSON.stringify(original));
deepCopy.details.age = 30;

console.log(original.details.age); // 25
console.log(deepCopy.details.age); // 30
```

In this example:
- We create a deep copy of `original` using `JSON.parse(JSON.stringify(original))`.
- All levels of the object are fully copied, not just the top level.
- Changing `deepCopy.details.age` does not affect `original.details.age`, as `deepCopy` is an entirely separate structure.

#### Common Ways to Make a Deep Copy
- **JSON.parse(JSON.stringify(object))**: Works well for simple, JSON-compatible objects but fails with complex data types (e.g., functions, dates, undefined).
- **Lodash’s `cloneDeep`**: A utility library that offers `_.cloneDeep`, which handles a variety of object types.
- **Manual deep copy function**: Writing a recursive function to handle deep cloning.

### Summary

| Aspect             | Shallow Copy                                        | Deep Copy                                         |
|--------------------|-----------------------------------------------------|---------------------------------------------------|
| **Nested Objects** | References to original nested objects               | Completely independent nested copies              |
| **Changes**        | Changes in nested objects affect both copies        | Changes in nested objects do not affect each other|
| **Common Methods** | Spread operator, `Object.assign`, `Array.slice`     | JSON methods, Lodash `cloneDeep`, recursive copy  |

### When to Use Each
- **Shallow Copy**: Good for flat objects, or if you don’t need to modify nested objects independently.
- **Deep Copy**: Necessary for complex objects where nested data should be modified independently without affecting the original structure.

Let me know if you need more clarification on any of these!
