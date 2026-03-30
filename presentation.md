

---

##  1. Importing and Exporting Modules

In Node.js, we use `require` and `module.exports` to share code between files.

### Exporting (math.js)

```js
function add(a, b) {
  return a + b;
}

module.exports = add;
```

### Importing (app.js)

```js
const add = require("./math");

const result = add(2, 3);
console.log(result);
```

###  Output

```
5
```

###  Simple Explanation

* `module.exports` → used to export a function or object
* `require()` → used to import it in another file

---

## 2. Console Methods

JavaScript provides different console methods for debugging.

###  console.log()

```js
console.log("Hello World");
```

**Output:**

```
Hello World
```

 Used for general output

---

### console.error()

```js
console.error("Something went wrong!");
```

**Output:**

```
Something went wrong!
```

 Used for errors (shown in red in console)

---

### console.info ()

```js
console.info("This is some info");
```

**Output:**

```
This is some info
```

 Used for informational messages

---

###  console.warn()

```js
console.warn("This is a warning");
```

**Output:**

```
This is a warning
```

Used for warnings

---

### console.table()

```js
const users = [
  { name: "John", age: 25 },
  { name: "Jane", age: 30 }
];

console.table(users);
```

**Output:**

```
(index)  name   age
0        John   25
1        Jane   30
```

Displays data in table format

---

##  3. Best Practices

###  3.1 Indentation

```js
//  Bad
if(true){
console.log("Hi");
}

//  Good
if (true) {
  console.log("Hi");
}
```

 Always use proper spacing (2 spaces or 4 spaces)

---

###  3.2 Variable Naming

```js
//  Bad
let x = 10;

// Good
let userAge = 10;
```

👉 Use meaningful names

---

###  3.3 Loop Variable Naming

```js
// Bad
for (let x = 0; x < arr.length; x++) {}

// Good
for (let i = 0; i < arr.length; i++) {}
```

 Use `i`, `j` for loops OR meaningful names like `index`

---

###  3.4 Use const and let properly

```js
//  Bad
var name = "John";

// Good
const name = "John"; // if value doesn't change
let age = 25;        // if value changes
```

---



###  3.5 Keep Functions Small

```js
//  Good
function greet(name) {
  return "Hello " + name;
}
```

 One function = one responsibility

---

###  3.6 Use Consistent Naming Style

```js
// camelCase for variables
let userName = "John";

// PascalCase for classes
class User {}
```

---

