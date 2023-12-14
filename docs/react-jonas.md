# Ultimate React Course by Jonas Schmedtmann

## Section 3: A First Look at React

### Pure React

- We learn how to use React without any build tool or package manager. We use the CDN links to React and Babel. We need to include 3 scripts in our HTML file:
  - React
  - ReactDOM
  - Babel
- We use the `type="text/babel"` attribute in our script tag to tell the browser that we are using JSX.
- We use the `ReactDOM.createRoot()` method to render our React app. This method is the new way of rendering React apps. The old way is to use the `ReactDOM.render()` method. The `createRoot()` method is more efficient and it is the recommended way of rendering React apps. We pass the `createRoot()` method the container element where we want to render our React app.

[Try React Locally](https://react.dev/learn/installation)

<details>
<summary>
HTML page from `react.dev` to try React locally
</summary>

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello World</title>
    <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>

    <!-- Don't use this in production: -->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

  </head>
  <body>
    <div id="root"></div>
    <script type="text/babel">

      function MyApp() {
        return <h1>Hello, world!</h1>;
      }

      const container = document.getElementById('root');
      const root = ReactDOM.createRoot(container);
      root.render(<MyApp />);

    </script>
    <!--
      Note: this page is a great way to try React but it's not suitable for production.
      It slowly compiles JSX with Babel in the browser and uses a large development build of React.

      Read this page for starting a new React project with JSX:
      https://react.dev/learn/start-a-new-react-project

      Read this page for adding React with JSX to an existing project:
      https://react.dev/learn/add-react-to-an-existing-project
    -->

  </body>
</html>

```

</details>

<details>
<summary>Code Explanation</summary>

```javascript
<script>
      function App() {
        return React.createElement("header", null, "Hello React Header");
      }

      const root = ReactDOM.createRoot(document.getElementById("root"));
      root.render(React.createElement(App));
</script>
```

`root.render(React.createElement(App)); `is doing two things:

- `React.createElement(App)` is creating an instance of the App component. This is the equivalent of writing `<App />` in JSX.

- `root.render(...)` is instructing React to render the instance of the `App` component into the root DOM node of your application.

</details>

> Pure React HTML

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>12-12-23 01-Pure React</title>
  </head>
  <body>
    <div id="root"></div>
    <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <script>
      function App() {
        return React.createElement("h3", null, "Hello React Header");
      }

      const root = ReactDOM.createRoot(document.getElementById("root"));
      root.render(React.createElement(App));
    </script>
  </body>
</html>

```

#### React useState and useEffect First Look

- We use the `React.useState()` hook to create a state variable. The `useState()` hook returns an array with two elements. The first element is the state variable and the second element is a function that we can use to update the state variable. We pass the initial value of the state variable to the `useState()` hook as an argument.
- `React.useEffect(...) ` is a hook that lets you perform side effects in function components. Side effects could be data fetching, subscriptions, or manually changing the DOM. In this case, the side effect is setting up an interval.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>12-12-23 01-Pure React</title>
  </head>
  <body>
    <div id="root"></div>
    <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <script>
      function App() {
        const [time, setTime] = React.useState(new Date().toLocaleTimeString());

        React.useEffect(function () {
          setInterval(function() {
            setTime(new Date().toLocaleTimeString())
          }, 1000);
        }, [])

        return React.createElement("h3", null, `Hello React! It is ${time}`);
      }

      const root = ReactDOM.createRoot(document.getElementById("root"));
      root.render(React.createElement(App));
    </script>
  </body>
</html>

```

- The first argument to useEffect is a function where you put the side effect code. This function will run after the render is committed to the screen. The function sets up an interval that runs every 1000 milliseconds (or 1 second). On each interval, it updates the state with the current time string.

- The second argument is an array of dependencies. If any of the dependencies change, the side effect function will run again. If you pass an empty array, the side effect function will only run once after the initial render.

- The side effect of this example is setting up an interval. The interval will run every 1000 milliseconds and update the state with the current time string. The side effect function will only run once after the initial render because we passed an empty array as the second argument. It is considered a side effect because it involves interacting with the outside world(in this case, the system's clock) and it changes the state of the component, which can lead to a re-render.

- Here's the process:

  1. The component renders for the first time.
  2. After the first render, the useEffect hook runs because it's called in the component.
  3. Inside the useEffect, setInterval is called. This sets up a timer that calls its callback function every 1000 milliseconds.
  4. Every 1000 milliseconds, the callback function to setInterval is called. This function updates the state with the current time string by calling setTime(new Date().toLocaleTimeString()).
  5. Updating the state causes the component to re-render, and the new time is displayed.
  6. Even though the component re-renders, the useEffect does not run again because its dependency array is empty. This means the setInterval is not set up again, and the existing interval continues to run.

- So, while the useEffect is only called once, the setInterval it sets up continues to run and update the state every second.

#### React Documentation

- [React Documentation](https://react.dev/learn)

### Setting Up a New React Project

#### The Two Options For Setting Up a New React Project

- We can use the `create-react-app` package to set up a new React project. This is the recommended way of setting up a new React project. It is the easiest way to get started with React. It sets up a React project with all the necessary dependencies and build tools. It also sets up a development server that automatically reloads the browser when you make changes to your code. It is the best way to get started with React. Use for tutorials or experiments. Do not use for real-world projects.
- We can also use `Vite` to set up a new React project. `Vite` is a new build tool that is very fast. It is a good alternative to `create-react-app`. It is a modern build tool that contains a template for setting up a React project. But we need to manually set up ESLint and others. It is extremely fast and it is good for real-world projects.

#### What about React Frameworks?

- `Next.js` and `Remix` are popular React Frameworks.

#### Create React App

Steps to set up a new React project with `create-react-app`:

1. use `npx create-react-app@5 my-app` to create a new React project. Replace `my-app` with the name of your project. `pizza-menu` is the name of the project in this example.
2. use `cd my-app` to change into the project directory.
3. use `npm start` to start the development server.
4. use `npm run build` to build the project for production.
5. use `npm run test` to run the tests.

The project is the same as the one we created using npm init and installing the dependencies manually. The only difference is that we didn't have to install the dependencies manually. The `create-react-app` package installed the dependencies for us. When checking the node_modules folder, we can see that `react` and `react-dom` are installed as dependencies. We included them using script tags in the previous example.

## Section 4 Review of Essential JavaScript for React

### Destructing Objects and Arrays

- Object destructing is a way to extract properties from an object and assign them to variables. We use the curly braces to destructure an object. We put the property names inside the curly braces. We can also rename the variables when destructuring an object. We use the colon to rename a variable. We put the new variable name before the colon and the old variable name after the colon. We can also set default values for the variables when destructuring an object. We use the equal sign to set a default value. We put the default value after the equal sign. `const {title, author} = book;` is the same as `const title = book.title; const author = book.author;`

- Array destructing is a way to extract items from an array and assign them to variables. We use the square brackets to destructure an array. We put the variable names inside the square brackets. We can also rename the variables when destructuring an array. We use the colon to rename a variable. We put the new variable name before the colon and the old variable name after the colon. We can also set default values for the variables when destructuring an array. We use the equal sign to set a default value. We put the default value after the equal sign. `const [first, second] = numbers;` is the same as `const first = numbers[0]; const second = numbers[1];`

```javascript

```

### Rest and Spread Operators

- The rest operator is used to get the remaining items in an array. We use the rest operator to get the remaining items in an array when destructuring an array. We use the rest operator to get the remaining items in an array when destructuring an array. `const [first, second, ...others] = numbers;` is the same as `const first = numbers[0]; const second = numbers[1]; const others = numbers.slice(2);`

- The spread operator is used to spread the items in an array. We use the spread operator to spread the items in an array when destructuring an array. `const newGenre = [...genres, "Thriller"];` will create a new array with the items in the genres array and the string "Thriller". `const newGenre = ["Thriller", ...genres];` will create a new array with the string "Thriller" and the items in the genres array. `const updatedBook = {...book, title: "New Title"};` will create a new object with the properties in the book object and the title property set to "New Title". \

- We can also use the spread operator to overwrite an existing property. `const updatedBook = {...book, movieReleaseDate: "2021-12-31", pages: 1210};` will create a new object with the properties in the book object and the movieReleaseDate property set to "2021-12-31". The pages property will also be overwritten and updated to 1210.

```javascript

```

### Template Literals

- Template literals are a way to create strings. We use the backtick `` to create a template literal. We can use the dollar sign and curly braces to insert a variable into a template literal. We can also use the dollar sign and curly braces to insert an expression into a template literal. We can also use the dollar sign and curly braces to insert a function call into a template literal. We can also use the dollar sign and curly braces to insert a ternary operator into a template literal.

```javascript

const summary = `${title} by ${author} has ${pages} pages.`;
const summary = `${title} by ${author} has ${pages} pages. ${pages > 500 ? "That's a long book!" : "That's a short book!"}`;

const summary = `${title}, a ${pages}-page long book, was written by ${author} and published in ${publicationDate.split("-")[0]}`;

```

### Arrow Functions

- Arrow functions are a way to create functions.
- The basic syntax is `const functionName = (parameters) => {function body}`.
- It has several special properties
  - It does not have its own `this` keyword. It inherit the `this` keyword from the the surrounding scope, which can be useful when working with object methods or event handlers.
  - No `arguments` object. We can use the rest operator(...args) to achieve the same functionality.
  - Cannot be used as constructors with the `new` keyword because they do not have the `prototype` property.

> `this` example

```javascript
function RegularFunction() {
  this.value = 1;
  setTimeout(function() {
    console.log(this.value); // undefined, because 'this' inside the function refers to the global object
  }, 100);
}

function ArrowFunction() {
  this.value = 1;
  setTimeout(() => {
    console.log(this.value); // 1, because 'this' inside the arrow function refers to the enclosing ArrowFunction object
  }, 100);
}

new RegularFunction(); // logs 'undefined'
new ArrowFunction(); // logs '1'
```

> arguments example

```javascript
function regularFunction() {
  console.log(arguments[0]); // logs 'hello'
}

const arrowFunction = (...args) => {
  console.log(args[0]); // logs 'hello'
};

regularFunction('hello', 'world');
arrowFunction('hello', 'world');
```

### Short-Circuiting and Logical Operators

- Short-circuiting is a way to write conditional statements in a shorter way.
- We use the `&&` operator to short-circuit the first falsy value. When the first value is falsy, it will return false without evaluating the second value. When the first value is truthy, it will return the second value.
- We use the `||` operator to short-circuit the first truthy value. When the first value is truthy, it will return true without evaluating the second value. When the first value is falsy, it will return the second value.
- falsy values: `false`, `0`, `""`, `null`, `undefined`, `NaN`.
- There may be some issue with `0` and `""` as falsy values. For example, we want to show the number of reviews of a book, when there is no review, we want to show "No reviews". But if the book has 0 reviews, we will show "No reviews" instead of "0 reviews." `const reviews = book.reviews || "No reviews";` will not work because `0` is a falsy value. `const reviews = book.reviews || book.reviews === 0 ? "No reviews" : book.reviews;` will work. But it is not a good solution.
- We can use the `??` operator to solve this problem. `const reviews = book.reviews ?? "No reviews";` will work. The `??` operator will return the second value if the first value is `null` or `undefined`. It will not return the second value if the first value is `0` or `""`.

```javascript

const b1 = true && "Hello"; // "Hello"
const b2 = false && "Hello"; // false

const b3 = false || "Hello"; // "Hello"
const b4 = true || "Hello"; // true

const reviews = book.reviews || "No reviews"; // wrong way
const reviews = book.reviews || book.reviews === 0 ? "No reviews" : book.reviews;
const reviews = book.reviews ?? "No reviews";

```

### Optional Chaining

- Optional chaining is a way to access properties of an object when the object may be null or undefined.
- We use the question mark `?` to access properties of an object when the object may be null or undefined. `const pages = book?.details?.pages;` will return `undefined` if `book` or `book.details` is `null` or `undefined`.

```javascript

function getTotalReviewCount(book) {
  const goodreads = book.reviews.goodreads?.reviewCount ?? 0;
  const libraryThing = book.reviews.libraryThing?.reviewCount ?? 0;
  return goodreads + libraryThing;

}

```

- JavaScript won't read the rest of the expression if the first part is `null` or `undefined`.
- We use `??` to set a default value for the expression. `const goodreads = book.reviews.goodreads?.reviewCount ?? 0;` will return `0` if `book.reviews.goodreads?.reviewCount` is `null` or `undefined`.

### The Array map Method

- The `map()` method creates a new array with the results of calling a function for every array element.
- The `map()` method calls the provided function once for each element in an array, in order.
- The `map()` method does not execute the function for array elements without values.
- The `map()` method does not change the original array.

```javascript

```

### The Array filter Method

### The Array reduce Method

### The Array sort Method

### Working with Immutable Arrays

### Asynchronous JavaScript: Promises

### Asynchronous JavaScript: Async/Await
