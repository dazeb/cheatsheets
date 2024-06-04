### JavaScript Basics
```javascript
// Variable Declarations
let variableLet = 'Let Variable';
const variableConst = 'Const Variable';
// Use `let` for mutable variables, `const` for constants

// Data Types
const str = "Hello, Next.js!";   // String
const num = 42;                 // Number
const bool = true;              // Boolean
const arr = [1, 2, 3];          // Array
const obj = { name: "Next" };   // Object

// Functions
function greet(name) {
    return `Hello, ${name}`;
}

// Arrow Functions
const sum = (a, b) => a + b;
```

### `var`

1. **Scope**: Function-scoped.
   - A `var` declaration is scoped to the function in which it is declared. If it's declared outside any function, it is global.
2. **Hoisting**: Yes, fully hoisted.
   - `var` declarations are hoisted to the top of their function scope and are initialized to `undefined`. Importantly, this means they can be referenced before they are declared.
3. **Redefinition and Reassignment**:
   - `var` can be redefined and reassigned within the same scope. This can sometimes lead to unexpected behaviors and bugs.

Example:
```javascript
function varExample() {
  console.log(x); // Undefined, due to hoisting
  var x = 5;
  console.log(x); // 5

  if (true) {
    var x = 10; // Redefines x in the same scope
    console.log(x); // 10
  }

  console.log(x); // 10, because x is redefined in the function scope
}

varExample();
```

### `let`

1. **Scope**: Block-scoped.
   - `let` is scoped to the block `{}` in which it is defined. This includes loops, conditionals, and any other block construct.
2. **Hoisting**: Yes, but not initialized.
   - `let` declarations are hoisted to the top of their block, but are not initialized until their declaration is encountered, leading to a `ReferenceError` if accessed before declaration.
3. **Redefinition and Reassignment**:
   - `let` can be reassigned but not redefined within the same scope. If you redeclare a variable declared with `let` in the same block, it will throw an error.

Example:
```javascript
function letExample() {
  // console.log(y); // ReferenceError: Cannot access 'y' before initialization
  let y = 5;
  console.log(y); // 5

  if (true) {
    let y = 10; // New y, scoped to this block
    console.log(y); // 10
  }

  console.log(y); // 5, because the y in the block does not affect this y
}

letExample();
```

### `const`

1. **Scope**: Block-scoped.
   - Similar to `let`, `const` is also block-scoped.
2. **Hoisting**: Yes, but not initialized.
   - `const` declarations are hoisted to the top of their block, but are not initialized until their declaration is encountered, leading to a `ReferenceError` if accessed before declaration.
3. **Redefinition and Reassignment**:
   - `const` cannot be reassigned or redefined within the same scope. Once a variable is defined with `const`, its value cannot change.
   - Note: For objects and arrays, `const` prevents reassignment of the variable itself, but the contents of objects/arrays can still be modified.

Example:
```javascript
function constExample() {
  // console.log(z); // ReferenceError: Cannot access 'z' before initialization
  const z = 5;
  console.log(z); // 5

  if (true) {
    const z = 10; // New z, scoped to this block
    console.log(z); // 10
  }

  console.log(z); // 5, because the z in the block does not affect this z

  // z = 15; // Error: Assignment to constant variable
}

constExample();

// Using const with Objects and Arrays
const obj = { name: 'John' };
obj.name = 'Jane'; // Allowed: modifying property
console.log(obj); // { name: 'Jane' }

// obj = {}; // Error: Assignment to constant variable

const arr = [1, 2, 3];
arr.push(4); // Allowed: modifying array content
console.log(arr); // [1, 2, 3, 4]

// arr = [5]; // Error: Assignment to constant variable
```

### Best Practices for Choosing `var`, `let`, and `const`

1. **Default to `const`**:
   - Use `const` for variables that should not be reassigned. This guards against accidental reassignments and reflects the intent that the variable is constant.

2. **Use `let` for variables that will change**:
   - If a variable's value needs to be updated later, use `let`. This clarifies that the variable is expected to be reassigned and helps avoid unexpected issues.

3. **Avoid `var`**:
   - Due to its function-scoping and hoisting behaviors, `var` can lead to bugs and harder-to-maintain code. Prefer `let` and `const` for more predictable scoping.

4. **Minimize scope leakage**:
   - Declare variables in the narrowest scope possible. This makes the code easier to read and maintain by keeping variable lifetimes explicit and reducing chances for unintended interactions.

5. **Understand Temporal Dead Zone (TDZ)**:
   - Both `let` and `const` are subject to the TDZ, which means they can't be accessed before their declaration within their scope. Be conscious of this to avoid `ReferenceError`.

### ES6+ Features
```javascript
// Destructuring
const user = { name: "John Doe", age: 30 };
const { name, age } = user;

// Spread Operator
const newUser = { ...user, email: 'john@example.com' };

// Template Literals
const greeting = `Hello, ${name}!`;

// Default Parameters
const increment = (val, by = 1) => val + by;

// Rest Parameters
### ES6+ Features (Continued)
```javascript
// Rest Parameters
const logValues = (...values) => {
  console.log(values);
};

// Modules
// Exporting
export const myFunction = () => {};

// Importing
// Import named exports
import { myFunction } from './myModule';

// Import default exports
import MyComponent from './MyComponent';
```

### 1. **Arrow Functions**

Arrow functions provide a shorter syntax for writing functions and lexically bind their `this` value, which avoids common issues with regular functions.

**Traditional function:**
```javascript
function add(a, b) {
  return a + b;
}
```

**Arrow function:**
```javascript
const add = (a, b) => a + b;
```

**Use cases:**
- Simplifying function syntax.
- Maintaining correct context for `this` in callbacks, especially within class methods.

### 2. **Template Literals**

Template literals provide a way to embed expressions within string literals using backticks (`` ` ``) and `${expression}` syntax. They also support multi-line strings.

**Traditional concatenation:**
```javascript
const name = 'John';
const greeting = 'Hello, ' + name + '!';
```

**Template literal:**
```javascript
const name = 'John';
const greeting = `Hello, ${name}!`;
```

**Use cases:**
- Making string interpolation more readable.
- Easily creating multi-line strings.

### 3. **Destructuring Assignment**

Destructuring allows you to unpack values from arrays or properties from objects into distinct variables.

**Array destructuring:**
```javascript
const rgb = [255, 100, 50];
const [red, green, blue] = rgb;
```

**Object destructuring:**
```javascript
const user = { name: 'Jane Doe', age: 25 };
const { name, age } = user;
```

**Use cases:**
- Simplifying code that extracts multiple properties from objects or arrays.
- Improving readability by more clearly stating what you expect from the structure.

### 4. **Default Parameters**

Default parameters allow you to specify default values for function parameters.

```javascript
function multiply(a, b = 1) {
  return a * b;
}
```

**Use cases:**
- Ensuring that a parameter always has a value.
- Avoiding the need to manually set default values within the function body.

### 5. **Rest and Spread Operators**

The rest operator (`...`) allows you to capture any number of arguments into an array, while the spread operator allows you to expand elements of an array or object.

**Rest operator:**
```javascript
// Function with rest parameters
const sum = (...numbers) => numbers.reduce((acc, current) => acc + current, 0);
```

**Spread operator:**
```javascript
// Spread elements in an array
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5]; // [1, 2, 3, 4, 5]

// Spread properties in an object
const user = { name: 'Jane Doe', age: 25 };
const updatedUser = { ...user, email: 'jane@example.com' }; // { name: 'Jane Doe', age: 25, email: 'jane@example.com' }
```

**Use cases:**
- Simplifying the collection of arguments.
- Cloning and merging arrays and objects.

### 6. **Classes**

JavaScript classes provide a more straightforward syntax for creating constructor functions and handling inheritance.

**Class definition:**
```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hello, my name is ${this.name}.`);
  }
}

const john = new Person('John', 30);
john.greet(); // Output: Hello, my name is John.
```

**Use cases:**
- Encapsulating data and functionality.
- Making object-oriented programming more intuitive.

### 7. **Enhanced Object Literals**

Enhanced object literals provide a more concise way to define object properties and methods.

```javascript
const name = 'Jane Doe';
const user = {
  name,
  greet() {
    console.log(`Hello, ${this.name}.`);
  }
};
```

**Use cases:**
- Reducing boilerplate when defining objects.
- Improving readability.

### 8. **Modules**

ES6 modules allow you to split your code into reusable pieces with `import` and `export` statements.

**Exporting:**
```javascript
// module.js
export const name = 'John Doe';
export function greet() {
  console.log('Hello!');
}
```

**Importing:**
```javascript
// main.js
import { name, greet } from './module.js';
console.log(name); // Output: John Doe
greet(); // Output: Hello!
```

**Use cases:**
- Encapsulating code into reusable modules.
- Encouraging code reuse and maintainability.

### 9. **Promises and Async/Await**

Promises and async/await provide a cleaner way to handle asynchronous operations compared to traditional callbacks.

**Promises:**
```javascript
const fetchData = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Data fetched');
    }, 1000);
  });
};

fetchData().then(data => console.log(data)).catch(err => console.error(err));
```

**Async/Await:**
```javascript
const fetchDataAsync = async () => {
  try {
    const data = await fetchData();
    console.log(data);
  } catch (err) {
    console.error(err);
  }
};

fetchDataAsync();
```

**Use cases:**
- Simplifying asynchronous logic.
- Improving readability and handling asynchronous errors more gracefully.

### 10. **Symbol**

Symbols provide a way to create unique identifiers, useful for object properties to avoid naming collisions.

```javascript
const sym1 = Symbol('description');
const sym2 = Symbol('description');
console.log(sym1 === sym2); // false

const obj = {
  [sym1]: 'value1',
  [sym2]: 'value2',
};

console.log(obj[sym1]); // Output: value1
console.log(Object.getOwnPropertySymbols(obj)); // [Symbol(description), Symbol(description)]
```

**Use cases:**
- Creating unique property keys.
- Avoiding property name conflicts in objects.

### 11. **Map and Set**

ES6 introduced new collections: `Map` and `Set`.

**Map:**
```javascript
const map = new Map();
map.set('key1', 'value1');
map.set('key2', 'value2');
console.log(map.get('key1')); // Output: value1
```

**Set:**
```javascript
const set = new Set([1, 2, 3, 4, 4]);
set.add(5);
console.log(set.has(1)); // true
console.log(set.size); // 5 (duplicates are ignored)
console.log([...set]); // [1, 2, 3, 4, 5]
```

**Use cases:**
- `Map` is useful for key-value storage with any type of keys.
- `Set` is useful for storing unique values.

### 12. **Optional Chaining and Nullish Coalescing (ES2020)**

**Optional Chaining (`?.`):**
Allows safe property access, returning `undefined` if the property does not exist.

```javascript
const user = {
  name: 'John',
  address: {
    city: 'New York',
  },
};

console.log(user?.address?.city); // New York
console.log(user?.contact?.phone); // undefined
```

**Nullish Coalescing (`??`):**
Provides a default value only if the left-hand side is `null` or `undefined`.

```javascript
const value = null ?? 'default'; // 'default'
const anotherValue = 0 ?? 'default'; // 0 (since 0 is not null or undefined)
```

**Use cases:**
- Avoiding errors when accessing deeply nested properties.
- Providing default values where `null` or `undefined` may appear.

### Conclusion

ES6+ features have significantly modernized JavaScript, making the language more powerful, expressive, and easier to work with. These features not only enhance the developer experience but also lead to more maintainable and readable code. Understanding and leveraging these newer capabilities will greatly improve your coding efficiency and is especially beneficial when working with advanced JavaScript frameworks like Next.js.

### Asynchronous JavaScript
```javascript
// Promises
const fetchData = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Data fetched");
    }, 1000);
  });
};

fetchData().then(data => {
  console.log(data);
}).catch(err => {
  console.error(err);
});

// Async/Await
const fetchDataAsync = async () => {
  try {
    const data = await fetchData();
    console.log(data);
  } catch (err) {
    console.error(err);
  }
};
```

### Concepts in Asynchronous JavaScript
1. **Callbacks**
2. **Promises**
3. **Async/Await**

### 1. **Callbacks**

A callback is a function passed as an argument to another function, to be executed after the completion of the asynchronous operation.

#### Example:
```javascript
function fetchData(callback) {
  setTimeout(() => {
    callback('Data fetched');
  }, 1000);
}

fetchData((data) => {
  console.log(data); // Outputs: Data fetched after 1 second
});
```

**Drawbacks:**
- **Callback Hell**: Nesting multiple asynchronous operations can make the code hard to read and maintain.
- **Error Handling**: Managing errors in deeply nested callbacks can become cumbersome.

#### Example of Callback Hell:
```javascript
doSomething(function(result1) {
  doSomethingElse(result1, function(result2) {
    doAnotherThing(result2, function(result3) {
      doFinalThing(result3, function(result4) {
        console.log(result4);
      });
    });
  });
});
```

### 2. **Promises**

Promises provide a more readable and maintainable way to handle asynchronous operations. A promise represents a value that may be available now, or in the future, or never.

#### States of Promises:
- **Pending**: Initial state, neither fulfilled nor rejected.
- **Fulfilled**: Operation completed successfully.
- **Rejected**: Operation failed.

#### Creating a Promise:
```javascript
const fetchData = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Data fetched');
    }, 1000);
  });
};
```

#### Consuming a Promise:
```javascript
fetchData()
  .then(data => {
    console.log(data); // Outputs: Data fetched after 1 second
  })
  .catch(error => {
    console.error(error); // Handles error
  })
  .finally(() => {
    console.log('Operation completed'); // Runs regardless of the outcome
  });
```

#### Chaining Promises:
Chaining allows sequential execution of asynchronous operations.
```javascript
fetchData()
  .then(data => {
    console.log(data);
    return fetchData(); // Chain another promise
  })
  .then(newData => {
    console.log(newData);
  })
  .catch(error => {
    console.error(error); // Catched any error in the chain
  });
```

### 3. **Async/Await**

`async/await` is syntactic sugar built on top of promises, making asynchronous code look more like synchronous code, which improves readability and maintainability.

#### Declaring an `async` function:
An `async` function always returns a promise.

```javascript
async function fetchDataAsync() {
  return 'Data fetched';
}

fetchDataAsync().then(data => console.log(data)); // Outputs: Data fetched
```

#### Using `await`:
`await` can be used to pause the execution of an `async` function until a promise is resolved or rejected.

```javascript
const fetchData = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Data fetched');
    }, 1000);
  });
};

async function fetchDataAsync() {
  try {
    const data = await fetchData();
    console.log(data); // Outputs: Data fetched after 1 second
  } catch (error) {
    console.error(error); // Handles error
  }
}

fetchDataAsync();

```

#### Sequential Execution:
Using `await`, you can easily perform sequential asynchronous operations.

```javascript
async function sequentialDataFetch() {
  const data1 = await fetchData();
  console.log(data1); // Outputs: Data fetched

  const data2 = await fetchData();
  console.log(data2); // Outputs: Data fetched
}

sequentialDataFetch();
```

#### Parallel Execution:
Using `Promise.all`, you can perform multiple asynchronous operations in parallel and wait for all of them to complete.

```javascript
async function parallelDataFetch() {
  const [data1, data2] = await Promise.all([fetchData(), fetchData()]);
  console.log(data1, data2); // Outputs: Data fetched Data fetched
}

parallelDataFetch();
```

### Error Handling

#### With Promises:
Errors are handled using the `.catch()` method.

```javascript
fetchData()
  .then(data => {
    throw new Error('Something went wrong');
  })
  .catch(error => {
    console.error(error.message); // Outputs: Something went wrong
  });
```

#### With Async/Await:
Error handling is done using `try...catch` blocks.

```javascript
async function fetchDataWithErrorHandling() {
  try {
    const data = await fetchData();
    console.log(data);
    throw new Error('Something went wrong');
  } catch (error) {
    console.error(error.message); // Outputs: Something went wrong
  }
}

fetchDataWithErrorHandling();
```

### Combining with Other ES6+ Features

#### Using Async/Await with Destructuring

```javascript
const fetchUserData = () => {
  return Promise.resolve({ name: 'John', age: 30 });
};

const fetchUserPosts = () => {
  return Promise.resolve([{ title: 'Post 1' }, { title: 'Post 2' }]);
};

async function getUserData() {
  try {
    const { name, age } = await fetchUserData();
    const [post1, post2] = await fetchUserPosts();

    console.log(name, age); // Outputs: John 30
    console.log(post1.title, post2.title); // Outputs: Post 1 Post 2
  } catch (error) {
    console.error(error);
  }
}

getUserData();
```

#### Using Async/Await with Template Literals

```javascript
async function displayUserData() {
  try {
    const user = await fetchUserData();
    console.log(`Name: ${user.name}, Age: ${user.age}`); // Outputs: Name: John, Age: 30
  } catch (error) {
    console.error(error);
  }
}

displayUserData();
```

### Conclusion

Asynchronous JavaScript is a cornerstone for modern web development. It enables non-blocking behavior crucial for building responsive applications. By mastering callbacks, promises, and `async/await`, you can write more efficient, readable, and maintainable asynchronous code.

### Next.js Specific Concepts

#### Routing
```javascript
// Pages are automatically routed based on file names
// File structure:
// ├── pages
// │   ├── index.js   // corresponding to '/'
// │   ├── about.js   // corresponding to '/about'
// │   └── [id].js    // dynamic route corresponding to any '/:id'

// Dynamic Routing
import { useRouter } from 'next/router';

const Post = () => {
  const router = useRouter();
  const { id } = router.query;

  return <div>Post: {id}</div>;
};

export default Post;
```

---
### 1. **Middleware**

Middleware in Next.js 14 allows you to run code before a request is completed. This can be very useful for things like authentication, logging, redirects, and more.

#### Example:
Create a middleware in `middleware.js` or `.ts`:
```javascript
import { NextResponse } from 'next/server';

export function middleware(request) {
  const url = request.nextUrl.clone();

  // Example: Redirect if the user is not authenticated
  if (!request.cookies.has('authenticated')) {
    url.pathname = '/login';
    return NextResponse.redirect(url);
  }

  // Continue with the next middleware or final response
  return NextResponse.next();
}

export const config = {
  matcher: ['/protected/path/:path*'],
};
```

### 2. **App Directory (App Router)**

The App Directory and the App Router in Next.js 14 provide a new way to structure and navigate your application, bringing more flexibility and better conventions.

#### Example:
The new structure typically involves organizing your component files within a `src/app` directory:

```plaintext
src/
├── app/
│   ├── layout.js 
│   ├── page.js
│   ├── [slug]/
│       └── page.js
```

- **`layout.js`**: Defines the layout for the entire application or specific sections.
- **`page.js`**: Acts as the main entry point for rendering content.

### 3. **Server Actions**

Server actions are a way to handle form submissions and similar tasks on the server side, removing the need for client-side JavaScript/Ajax.

#### Example:
```javascript
// pages/api/contact.js

export default async function handler(req, res) {
  if (req.method === 'POST') {
    const { name, email, message } = req.body;

    // Handle the data, contact a database, etc.
    await saveToDatabase({ name, email, message });

    res.status(200).json({ message: 'Success' });
  } else {
    res.status(405).json({ message: 'Method not allowed' });
  }
}
```

### 4. **Image Optimization**

Next.js 14 continues to improve on the built-in Image Optimization API to make your images load more efficiently and responsively.

#### Example:
```javascript
import Image from 'next/image';

const MyComponent = () => (
  <Image 
    src="/images/my-image.jpg" 
    alt="My Image" 
    width={600} 
    height={400} 
    placeholder="blur" // Use blur-up placeholder
    layout="responsive" // Responsive layout
  />
);
```

### 5. **Edge Functions**

Edge functions allow you to run serverless functions closer to the user, minimizing latency by executing at the edge network.

#### Example:
```javascript
// edge.js

import { NextResponse } from 'next/server';

export default async function handler(req) {
  return NextResponse.json({
    message: 'Hello from the edge!',
  });
}

export const config = {
  runtime: 'edge',
};
```

### 6. **Static and Dynamic Rendering**

Next.js 14 introduces more nuanced options for static and dynamic rendering, giving you greater control over how and when your pages are rendered and cached.

- **Static Generation** (`getStaticProps`): Pre-renders pages at build time.
- **Server-Side Rendering** (`getServerSideProps`): Pre-renders on each request.
- **Incremental Static Regeneration (ISR)**: Revalidate pages at a set interval.
- **On-Demand ISR**: Update static content on demand via an API endpoint.

#### Example using `getStaticProps`:
```javascript
// pages/products/[id].js

export async function getStaticPaths() {
  const paths = await getProductIds();
  return {
    paths,
    fallback: 'blocking',
  };
}

export async function getStaticProps({ params }) {
  const product = await getProductById(params.id);
  return {
    props: {
      product,
    },
    revalidate: 10, // Revalidate at most every 10 seconds
  };
}

const ProductPage = ({ product }) => (
  <div>
    <h1>{product.name}</h1>
    <p>{product.description}</p>
  </div>
);

export default ProductPage;
```

### 7. **Advanced Routing**

Next.js 14 introduces more advanced routing capabilities, such as parallel routes and nested layouts. This allows for complex navigational scenarios like sidebars, nested content, and more.

#### Example:
```jsx
// app/layout.js
export default function RootLayout({ children }) {
  return (
    <html>
      <head />
      <body>
        <NavMenu /> // Sidebar or navigation menu
        <div>{children}</div>
      </body>
    </html>
  );
}

// app/dashboard/layout.js
export default function DashboardLayout({ children }) {
  return (
    <div>
      <DashboardHeader />
      <main>{children}</main>
    </div>
  );
}
```

### 8. **Webpack 5 + SWC**

Next.js 14 defaults to Webpack 5 and uses SWC (a super-fast TypeScript/JavaScript compiler) for faster builds and better performance.

#### Benefits:
- Faster builds and minification.
- Enhanced tree-shaking and code splitting.
- Better caching strategies.

### 9. **Script Component**

Next.js 14 enhances the `<Script>` component, enabling more control over third-party scripts, including better support for loading priority and strategy.

#### Example:
```javascript
import Script from 'next/script';

const MyPage = () => (
  <>
    <Script 
      src="https://example.com/some-script.js"
      strategy="lazyOnload"
      onLoad={() => console.log('Script has loaded!')}
    />
    <main>Page content...</main>
  </>
);
```

### 10. **Internationalization (i18n)**

Next.js 14 includes improved internationalization (i18n) support, allowing applications to easily handle multiple languages and locales.

#### Example:
```javascript
// next.config.js

module.exports = {
  i18n: {
    locales: ['en-US', 'fr', 'nl-NL'],
    defaultLocale: 'en-US',
    localeDetection: true,
  },
};
```

### 11. **Compiler Options**

Next.js 14 offers more advanced compiler options with SWC for customizing how your code is transformed.

#### Example:
```javascript
module.exports = {
  swcMinify: true,
  swcPlugins: [
    ['@swc/plugin-transform-react-jsx'],
    ['@swc/plugin-optimize-react'],
  ],
};
```

### Conclusion

Next.js 14 introduces a plethora of new and refined features that enhance performance, developer experience, and flexibility. By understanding and leveraging these concepts, you can create highly efficient, scalable, and maintainable applications. Whether you’re optimizing image loads, handling complex routing, or running functions at the edge, Next.js 14 offers the tools you need to build next-generation web applications.

#### API Routes
```javascript
// API routes can be created by adding files to the 'pages/api' directory
// File: pages/api/hello.js
export default function handler(req, res) {
  res.status(200).json({ message: 'Hello, Next.js!' });
}
```

#### Data Fetching
```javascript
// getStaticProps - Fetch data at build time
export async function getStaticProps() {
  const data = await fetchData();
  return {
    props: {
      data,
    },
  };
}

// getServerSideProps - Fetch data on each request
export async function getServerSideProps() {
  const data = await fetchData();
  return {
    props: {
      data,
    },
  };
}
```

#### CSS Modules and Styled JSX
```javascript
// CSS Modules
import styles from './Home.module.css';

export default function Home() {
  return <div className={styles.container}>Hello, World!</div>;
}

// Styled JSX
export default function Home() {
  return (
    <div>
      Hello, World!
      <style jsx>{`
        div {
          color: red;
          font-size: 20px;
        }
      `}</style>
    </div>
  );
}
```

#### API Integration
```javascript
// Using 'axios' for API Calls
import axios from 'axios';

export async function getServerSideProps() {
  const response = await axios.get('https://api.example.com/data');
  const data = response.data;

  return {
    props: { data }
  }
}

const DataDisplay = ({ data }) => {
  return (
    <div>
      <h1>Fetched Data</h1>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </div>
  );
}

export default DataDisplay;
```

#### Using Environment Variables
```javascript
// Create a ".env.local" file in the root directory
// .env.local
NEXT_PUBLIC_API_URL=https://api.example.com

// Access Environment Variables
const apiUrl = process.env.NEXT_PUBLIC_API_URL;
```

#### Image Optimization
```javascript
import Image from 'next/image';

export default function Home() {
  return (
    <div>
      <Image 
        src="/vercel.svg" 
        alt="Vercel Logo" 
        width={72} 
        height={16} 
      />
    </div>
  );
}
```

#### Custom App Component
```javascript
// pages/_app.js
import '../styles/globals.css'

function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />
}

export default MyApp
```

#### Custom Document Component
```javascript
// pages/_document.js
import Document, { Html, Head, Main, NextScript } from 'next/document'

class MyDocument extends Document {
  render() {
    return (
      <Html>
        <Head>
          {/* Custom fonts or meta tags */}
        </Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    )
  }
}

export default MyDocument
```

---

### JavaScript Basics and Best Practices
#### Variable Declarations and Scope
```javascript
// Variables declared with 'let' and 'const' are block-scoped
// Avoid using 'var' as it is function-scoped and can lead to unexpected behavior

let variableLet = 'Let Variable'; // Block-scoped
const variableConst = 'Const Variable'; // Read-only, block-scoped

// Avoid these pitfalls:
// var variableVar = 'Var Variable'; // Function-scoped
```

### Variable Declarations in JavaScript

JavaScript allows declaring variables with three primary keywords: `var`, `let`, and `const`. Each has unique properties and rules around scope and reassignment.

#### `var`
- Function-scoped: A `var` declared variable is accessible within the function it is defined in.
- Can be redeclared and reassigned: `var` allows you to redeclare the same variable multiple times (which can lead to bugs).
- Hoisting: `var` variables are hoisted to the top of their functional scope but initialized to `undefined`.

Example:
```javascript
function exampleVar() {
  var x = 10;
  if (true) {
    var x = 20; // Redefines x in the same scope
    console.log(x); // Outputs: 20
  }
  console.log(x); // Also outputs: 20
}

exampleVar();
```

#### `let`
- Block-scoped: `let` variables are only accessible within the block (denoted by `{}`) they are declared in.
- Cannot be redeclared in the same scope but can be reassigned.
- Hoisting: `let` variables are hoisted to the top of their block, but not initialized, leading to a `ReferenceError` if accessed before declaration.

Example:
```javascript
function exampleLet() {
  let x = 10;
  if (true) {
    let x = 20; // Block-scoped
    console.log(x); // Outputs: 20
  }
  console.log(x); // Outputs: 10
}

exampleLet();
```

#### `const`
- Block-scoped: Similar to `let`, `const` variables are only accessible within the block they are defined in.
- Cannot be redeclared or reassigned: `const` defines a constant reference, although the value of an object or array referenced by `const` can still be modified.
- Hoisting: `const` variables are hoisted to the top of their block but not initialized.

Example:
```javascript
function exampleConst() {
  const x = 10;
  // x = 20; // Error: Assignment to constant variable

  const arr = [1, 2, 3];
  arr.push(4); // Allowed, as we are modifying the contents, not the reference
  console.log(arr); // Outputs: [1, 2, 3, 4]
}

exampleConst();
```

### Scope

#### Global Scope
Variables defined outside any function or block are in the global scope and accessible anywhere in the code.

Example:
```javascript
let globalVar = 'I am global';

function exampleGlobalScope() {
  console.log(globalVar); // Accessible
}

exampleGlobalScope();
```

#### Function Scope
Variables declared within a function using `var`, `let`, or `const` are only accessible within that function.

Example:
```javascript
function exampleFunctionScope() {
  let functionVar = 'I am local to this function';
  console.log(functionVar); // Accessible within the function
}

exampleFunctionScope();
// console.log(functionVar); // Error: functionVar is not defined
```

#### Block Scope
Variables declared with `let` or `const` within a block (denoted by `{}`) are only accessible within that block.

Example:
```javascript
function exampleBlockScope() {
  if (true) {
    let blockVar = 'I am local to this block';
    console.log(blockVar); // Accessible within the block
  }
  // console.log(blockVar); // Error: blockVar is not defined
}

exampleBlockScope();
```

#### Lexical Scope (Closures)
JavaScript functions form closures, meaning they have access to variables from their parent scope even after the parent function has executed.

Example:
```javascript
function outerFunction() {
  let outerVar = 'I am from outer function';

  function innerFunction() {
    console.log(outerVar); // Accessible due to closure
  }

  innerFunction();
}

outerFunction();
```

### Best Practices

1. **Use `const` by default**:
   - Use `const` for variables that won't be reassigned. It signals that the variable is a constant reference and helps avoid unintentional reassignments.

2. **Use `let` for variables that will change**:
   - When you know the value of a variable will change, use `let`. It clearly communicates the intention to reassign the variable.

3. **Avoid `var`**:
   - Using `var` can lead to unintended side effects because of its function-scoping and hoisting behavior.

4. **Scope Functions and Variables**:
   - Keep variables as local as possible to avoid polluting the global scope and reduce potential conflicts or side effects.

5. **Understand and Leverage Closures**:
   - Closures can be powerful but understand them well to avoid memory leaks and unexpected behavior.

#### Primitive and Reference Data Types
```javascript
// Primitive Types
const str = 'Hello, Next.js!';
const num = 42;
const bool = true;
const undf = undefined; // Explicitly undefined
const nll = null; // Null value
const sym = Symbol('symbol'); // Unique symbol

// Reference Types
const arr = [1, 2, 3]; // Array
const obj = { name: 'Next' }; // Object
```

#### Functions and Arrow Functions
```javascript
// Function Declaration
function greet(name) {
    return `Hello, ${name}`;
}

// Function Expression
const greetFunc = function(name) {
    return `Hello, ${name}`;
};

// Arrow Function
const greetArrow = name => `Hello, ${name}`;

// Higher-order functions
const applyFunc = (func, value) => func(value);

// Example usage
applyFunc(greet, 'Next.js');
```

#### ES6+ Advanced Features

##### Destructuring Assignment
```javascript
// Object Destructuring
const user = { name: 'John Doe', age: 30, address: { city: 'NY' } };
const { name, age, address: { city } } = user; // Nested destructuring

// Array Destructuring
const arr = [1, 2, 3];
const [first, second, third] = arr; // Destructuring arrays
```

##### Spread and Rest Operators
```javascript
// Spread Operator in Objects
const userDetails = { ...user, email: 'john@example.com' };

// Spread Operator in Arrays
const newArr = [...arr, 4, 5, 6];

// Rest Operator in Function Parameters
const logValues = (...values) => {
  console.log(values);
};

// Rest Operator in Destructuring
const [first, ...rest] = newArr; // 'rest' is [2, 3, 4, 5, 6]
```

##### Enhanced Object Literals
```javascript
// Property Shorthands
const name = 'John Doe';
const user = { name };

// Method definitions in object literals
const obj = {
  greet() {
    console.log('Hello');
  }
};
```

#### Async Programming with Promises and Async/Await

##### Promises
```javascript
const fetchData = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Data fetched');
    }, 1000);
  });
};

fetchData()
  .then(data => console.log(data))
  .catch(err => console.error(err));
```

##### Async/Await
```javascript
const fetchDataAsync = async () => {
  try {
    const data = await fetchData();
    console.log(data);
  } catch (err) {
    console.error(err);
  }
};

fetchDataAsync();
```

### Next.js Specific Concepts and Best Practices

#### File-based Routing
```javascript
// File structure:
// ├── pages
// │   ├── index.js   // Maps to '/'
// │   ├── about.js   // Maps to '/about'
// │   └── blog
// │       ├── index.js // Maps to '/blog'
// │       └── [id].js  // Dynamic route '/blog/:id'

// Dynamic Routing Example
import { useRouter } from 'next/router';

const Post = () => {
  const router = useRouter();
  const { id } = router.query;

  return <div>Post: {id}</div>;
};

export default Post;
```

#### API Routes
```javascript
// Create API routes in 'pages/api'
// API route example: pages/api/hello.js

// API handler function
export default function handler(req, res) {
  // Handle GET request
  if (req.method === 'GET') {
    res.status(200).json({ message: 'Hello, Next.js!' });
  } else {
    res.status(405).json({ message: 'Method Not Allowed' });
  }
}
```

#### Data Fetching

##### Static Site Generation (SSG) with `getStaticProps`
```javascript
// Fetch data at build time
export async function getStaticProps() {
  const data = await fetchData();
  return {
    props: {
      data,
    },
    revalidate: 10, // Optional, revalidate every 10 seconds
  };
}

const HomePage = ({ data }) => {
  return <div>{data}</div>;
};

export default HomePage;
```

##### Server-side Rendering (SSR) with `getServerSideProps`
```javascript
// Fetch data on every request
export async function getServerSideProps() {
  const data = await fetchData();
  return {
    props: {
      data,
    },
  };
}

const HomePage = ({ data }) => {
  return <div>{data}</div>;
};

export default HomePage;
```

##### Incremental Static Regeneration (ISR)
```javascript
// Use SSG with revalidation (ISR)
export async function getStaticProps() {
  const data = await fetchData();
  return {
    props: {
      data,
    },
    revalidate: 60, // Revalidate at most every 60 seconds
  };
}
```

#### CSS Modules and Styled JSX
```javascript
// Utilize CSS Modules for scoped CSS
import styles from './Home.module.css';

const HomePage = () => {
  return <div className={styles.container}>Hello, World!</div>;
};

export default HomePage;

// Utilize Styled JSX for scoped CSS-in-JS
const HomePage = () => {
  return (
    <div>
      Hello, World!
      <style jsx>{`
        div {
          color: red;
          font-size: 20px;
        }
      `}</style>
    </div>
  );
};

export default HomePage;
```

#### API Integration with Axios
```javascript
import axios from 'axios';

export async function getServerSideProps() {
  const response = await axios.get('https://api.example.com/data');
  const data = response.data;

  return {
    props: { data },
  };
}

const DataDisplay = ({ data }) => {
  return (
    <div>
      <h1>Fetched Data</h1>
      <pre>{JSON.stringify(data, null, 2)}</pre>
    </div>
  );
};

export default DataDisplay;
```

#### Using Environment Variables
```javascript
// Create a ".env.local" in the root directory
// .env.local
NEXT_PUBLIC_API_URL=https://api.example.com

// Accessing Environment Variables in your components/pages
const apiUrl = process.env.NEXT_PUBLIC_API_URL;
```

#### Image Optimization with `next/image`
```javascript
import Image from 'next/image';

const HomePage = () => {
  return (
    <div>
      <Image 
        src="/vercel.svg" 
        alt="Vercel Logo" 
        width={72} 
        height={16} 
      />
    </div>
  );
};

export default HomePage;
```

#### Custom App Component for Global Styles
```javascript
// pages/_app.js
import '../styles/globals.css';
import { useEffect } from 'react';

function MyApp({ Component, pageProps }) {
  useEffect(() => {
    // Global client-side logic
  }, []);

  return <Component {...pageProps} />;
}

export default MyApp;
```

#### Custom Document for Extended HTML
```javascript
// pages/_document.js
import Document, { Html, Head, Main, NextScript } from 'next/document';

class MyDocument extends Document {
  render() {
    return (
      <Html>
        <Head>
          {/* Add custom fonts or meta tags */}
        </Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    )
  }
}

export default MyDocument;
```

#### TypeScript Integration
```typescript
// TypeScript support in Next.js is effortless
// Step 1: Install TypeScript
// npm install --save-dev typescript @types/react @types/node

// Step 2: Create a TypeScript configuration file
// touch tsconfig.json

// TypeScript Example: pages/index.tsx
import { NextPage } from 'next';

interface Props {
  title: string;
}

const HomePage: NextPage<Props> = ({ title }) => {
  return <h1>{title}</h1>;
};

export async function getStaticProps() {
  return {
    props: {
      title: 'Welcome to Next.js with TypeScript!',
    },
  };
}

export default HomePage;
```
