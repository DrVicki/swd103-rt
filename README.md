# L01HandsOnAssignment

### L01 Hands On Guided Learning: Build the Greeting App

Welcome to your very first React hands-on practice assignment, as part of this React Course.

The first real example you will build is a really simple greeting app that’s going to accept a `name` in an `input` box and output it back as part of a welcoming message.

### Requirements

1. Read all the guided learning text carefully for understanding.
2. Follow all instructions and coding step-by-step.
3. Create all files and folders for the Greeting App.
4. Complete all coding as demonstrated in all files.
5. Download Project Folder.
6. Zip `L01ReactHandsOn` Folder
7. Attach the zipped folder below where indicated for submission.

#### [Get Starter Code Replit](https://stackblitz.com/edit/reactstartercode?file=src%2FApp.js)

**Note** You don’t need to do any configuration to make it work, because you’re using `Parcel`.

What you find with most real-life React projects is they will be adding the React libraries with `npm` and usually use a code bundler such as `Webpack`, or even the Create React App starter project (which uses `Webpack` under the hood).

#### Check `packkage.json` for React Dependencies

3. There are two packages you need; `React`, and `React DOM`.

* `React` is the star of the show and includes the core `React` library.
* `React DOM` is a secondary package responsible for rendering `components` to the `DOM` in the browser.
* `parcel-bundler`

[![](https://github.com/DrVicki/swd103-rt/raw/main/Lesson-1/Lesson-1-Media/react-dependencies.png)](Lesson-1/Lesson-1-Media/react-dependencies.png)

### Code the Project Files

On to the exciting part: build out your app! For smaller projects like this, just start by creating all the files you need, and then filling them in as you go along.

For your greeting app, you need four files. You'll need:

1. A **styl**s file, called `styles.css`. You just have some basic styles to make your app look slightly more interesting than the out-of-the-box HTML.
2. Your **Parcel** starting point, `index.html`. This is the very first entry point Parcel is going to look for to `render` your app.
3. A starting point for the JavaScript, which will be `index.js`.
4. And finally, your main React component, which you call `App.js`. This is your main entry point for the React side of things.

After you review these files, fill them in. Start with your `style.css` file.

#### Style.css

Your styles file isn’t absolutely essential at this point, but it’s nice to have a few basic styles improve the built-in look and feel browsers give by default.

```
body {
  font-size: 16px;
  line-height: 1.4;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande',
    'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
  margin: 5em;
}

p {
  margin-bottom: 1.6em;
}

input {
  padding: 0.5em 1em;
  line-height: 1;
  font-size: 18px;
  border: 1px solid #ececec;
}

button {
  border: 1px solid #ececec;
  background: #ececec;
  padding: 0.5em 1em;
  cursor: pointer;
  font-size: 18px;
}

button:hover {
  background: #c9c6c6;
}
```

You see some simple styles that just affect the `body`, `font size`, and `line-height`. Later, you add an `input` and a `button` to your app, so you also added some nice styles for those.

'Save' and move to your entry point; your `index.html` file.

#### index.html

Add `HTML` to your `index.html` file.

```
<html>
  <head>
    <title>L01 React Example</title>
  </head>
  <body>
    <div id="root"></div>
    <script src="index.js"></script>
  </body>
</html>
```

Add the `HTML` tag first. Inside that, add a `<head>` tag, and within that, add a `<title>` tag. Give it a `title` of ‘`My first React example`’.

You need a `<body>` tag, so add that. Within the `<body>` tag, you need two things:

1. An element to render your React output into.
2. A script tag to reference your JavaScript entry point, `index.js` (which you create once you’re done here).

For the first one, add a `<main>` element and give it an `ID` of ‘`output`’. Finally, add your `<script>` tag that references `index.js`.

When `Parcel` runs, it looks in the `index.html` file first for any `script` tags. When it finds one pointing to `index.js`, it looks there to see what other JavaScript files it needs to import and chain together, to bundle into your working app.

#### index.html contents

```
<html>
  <head>
    <title>L01 React Example</title>
  </head>
  <body>
    <div id="root"></div>
    <script src="index.js"></script>
  </body>
</html>
```

Save the file and move to the main JavaScript entry point; the `index.js` file.

### index.js

Inside your `index.js` file is where the magic happens. It’s the first place you really set up your React app to load and inject content into your `HTML` page. This is going to be a small file where you add your very first piece of React code.

We will do a few things inside this file:

1. Import `React`
2. Import your main App `component`; the starting point for your React app
3. Use `React DOM` to `render` your App to the browser

#### Import React and the App Component

Import two React packages: `React` and `React DOM`.

**index.js**

```
import React from 'react';
import ReactDOM from 'react-dom/client';
import { createRoot } from 'reacr-dom/client;
​
import App from './App';
```

**Note**

When doing anything with React, you must import it at the **top** of the file.

* This is bringing React into **scope**.

For this file, you need the `React-DOM/client` package, which is responsible for rendering React code to the browser.

Import your `App` component, which will complete greeting the user.

Make sure your app gets rendered to the browser. To do that, call the `render` method from the `react-Dom/client` package you imported.

**index.js**

```
const rootElement = document.getElementById('root');
const root = createRoot(rootElement);

root.render(
  <>
    <App />
  </>
);
```

`root.render()` accepts two arguments:

1. The component you want to render (`APP`).
2. Where you want to render it, i.e. the '`root`' `div` in your `HTML` element from the `index.html` file.

To add your `App` component into the `root.render()` method, get your first peep of `JSX`, React’s XML-like syntax. It looks very similar to `XML` or `HTML` and later on, you add `paragraph` tags and `input` elements into your components. It’s important to know the difference. What you’re using here is `JSX` which is propriety `React` syntax.

For the second part, use the built-in `document.getElelmentById` method to find the `<root>` element you created in your `index.html` file. You gave it an `ID` of `output` so you’ll use that here to find it.

Save the file and move to your `App` component.

**index.js (now)**

```
import React from 'react';
import ReactDOM from 'react-dom/client'
import { createRoot } from 'react-dom/client';

import App from './App';

const rootElement = document.getElementById('root');
const root = createRoot(rootElement);

root.render(
  <>
    <App />
  </>
);
```

#### App.js

**Note**

The name of the file has been capitalized to ‘`App.js`’. This is not 100% necessary, but it’s a convention used among React projects to capitalize any component file names.

The last piece of the puzzle is to build out your `App` component to make something happen and greet your users.

If you use React, you need to have React in scope. Import React at the top of the file.

**App.js**

```
import React from 'react';
import './style.css';
```

#### Scaffold the app

Outline the basics of the component and then export that component so it can be used in another file, or another component.

It will look like this:

```
import React from 'react';
import './style.css';

class App extends Component {
  // TODO - implement component contents
}

export default App;
```

Use a class-based component, an older less-preferable means to build components. However, you’ll see them out in the wild, so it’s useful to take a look at how they’re built. For future lessons, you use the more modern functional components with **React Hooks** which look quite different.

For **class-based** components, you `extend` React’s Component class. Type the `extends` keyword after your class declaration, and then extend the `Component` class there.

To make this look a little cleaner, change the `import React` to the `Component` class as part of your React import at the top of the file. Change it to a named import like this:

**App.js**

`import React, { Component } from 'react';`

By doing that, you replace the `React.Component` part with just `Component`.

Finally, add a `default export` at the bottom for this component which is just `App`. Add this right after your class declaration as above.

**App.js**

`export default App;`

You’re not quite finished yet, but have the building blocks in. If you run this now, nothing would happen because your component doesn’t return anything.

#### Add a Title

All React components have to provide a `return` which is usually a block of `JSX`. With class-based components, you have to first provide a `render()` method and then add a `return` statement within the `render()` method.

To get started and to test your app, return a `heading`. Add a `render()` method, add a `return` statement within that, and add a simple message using an `<h1>` tag.

**App.js**

```
import React, { Component } from 'react';
import './style.css';

class App extends Component {
  // TODO - implement component contents
}


render() {
 return (
  <h1>Welcome to the app</h1>
 );
}


export default App;
```

The browser display should should show your lovely welcome message, ‘`Welcome to the app`’.

[![](https://github.com/DrVicki/swd103-rt/raw/main/Lesson-1/Lesson-1-Media/welcome-to-app.png)](Lesson-1/Lesson-1-Media/welcome-to-app.png)

**Tip!**

Another nice thing about Parcel’s local development server is hot reloads, responding to file changes on saving and refreshing the browser!

#### Prevent JSX errors with React Fragments

An important thing to note about `JSX` is you can only return one top-level element. To highlight this, if you type a `paragraph` tag in here and say ‘`this is a paragraph`’, then click save, you'll see we get a nasty error message.

[![](https://github.com/DrVicki/swd103-rt/raw/main/Lesson-1/Lesson-1-Media/lesson\_01-jsx-error.png)](Lesson-1/Lesson-1-Media/lesson\_01-jsx-error.png)

The error message states ‘`Adjacent JSX elements must be wrapped in an enclosing tag. Did you want to use a JSX fragment?`’

You have adjacent, top-level elements in your `return` statement. To fix this, wrap these elements in a containing element.

For these cases, use the `React.Fragment` syntax. Use the `React.Fragment` syntax or its shorthand:

**index.html**

```
// both of these statements are equal
render() {
    return (

 <h1>Welcome to the app</h1>
 <p>Hi there!</p>

   );
  }
}

export default App;
```

or

```
 render() {
    return (

<>
 <h1>Welcome to the app</h1>
 <p>Hi there!</p>
</>
    );
  }
}

export default App
```

The shorthand version (latter) looks much neater and cleaner. Use this version wherever it’s needed.

**Note!**

`React` and the `DOM`: React uses its own copy of the `DOM` which is called the **Virtual DOM**. React handles changes to this internal copy of the `DOM` and the real `DOM` in the browser to keep everything in sync. Although `JSX` looks almost identical to the same HTML you’d type into a `.html` file, it’s important to understand it doesn’t map directly to the `HTML` that’s eventually output to the browser.

#### Add a Dynamic Message

Expand your app. In the first paragraph, return user's name once they type it in. Modify paragraph tag to include some executable code.

**App.js**

```
render() {
    return (
      <>
        <h1>Welcome to the app</h1>
        <p>
          Hi there, {this.state.displayName || "we haven't been introduced"}
        </p>
```

Notice a call to a class property called `state`. Each component has access to its `state` and its `local storage`. You store values in a `state` as well as retrieve them, which is what you’re doing here.

Your line, `{this.state.displayName}` is really saying ‘get me the `displayName` value out of this component’s `state`’.

You haven't added your `state` yet, so do that now.

#### Add State to Your app

Within a class-based component, just like a regular JavaScript class, initialize any state values in the constructor.

**App.js**

```
iimport React, { Component } from 'react';
import './style.css';

class App extends Component {
  constructor(props) {
    super(props);

    this.state = {
      name: '',
      displayName: ''
    };
  }
```

React automatically wires up your constructor when the component is created, and it passes it a properties object, called `props` for short (you see this often when dealing with React).

The first thing to do in your constructor is call the parent class constructor (the parent class is the Component class you extended right at the beginning) using `super` method, passing in the `props` object.

To add your component’s `state` property, simply call `this.state` and set it to an object that contains whatever data you need it to. For now, just add the `displayName` property and set it to an empty string.

**Note!**

An important thing to know about `state` is that it is **immutable**. This means it can be updated by using React’s `setState()` method, but never edit `state` directly. The only time you ever set `state` directly is in a constructor.

You don’t have to initialize `state` in the constructor as you’re doing here, but it’s a good habit to get into so anyone coming into the class can see what properties should be expected to exist on the `state object`, and what their `values` or their `types` should be.

#### Handle User Input

You have your dynamic welcome message, but you need to allow the user to enter their name so you can greet them personally.

Add some instructions and an input box:

**App.js**

```
render() {
    return (
      <>
        <h1>Welcome to the app</h1>
        <p>
          Hi there, {this.state.displayName || "we haven't been introduced"}
        </p>
        <p>Enter your name below so we can get better acquainted</p>
        <input value={this.state.name} onChange={this.handleChange} />
        <button onClick={this.handleClick}>Update name</button>
      </>
    );
  }
}

export default App;
```

Set your input’s `value` to another `state` value, `{this.state.name}`. By doing this you turn it into a controlled component. HTML form elements like `input`s, `select`s, and `text` areas are typically uncontrolled components because they handle their own `state` and `values`.

By letting React handle your input’s `value` from `state`, it becomes a controlled component, which means React is responsible for maintaining the `state` of any `value` we assign to it.

Since you added a new `state` value reference here, update your component’s `state` in the constructor:

**App.js**

```
import React, { Component } from 'react';
import './style.css';

class App extends Component {
  constructor(props) {
    super(props);

    this.state = {
      name: '',
      displayName: ''
    };
  }
```

If you stop there, however, the value of the input will always be an empty string. You need a way to update this `value` in `state` whenever someone updates the text.

Add an event handler to the `input` element. The perfect place to do this update will be as part of the `onChange` event, which fires every time the text in the `input` changes.

Add the `onChange` event to the `input` and add a handler function, `handleChange` which you define next.

**App.js**

```
        render() {
    return (
      <>
        <h1>Welcome to the app</h1>
        <p>
          Hi there, {this.state.displayName || "we haven't been introduced"}
        </p>
        <p>Enter your name below so we can get better acquainted</p>
        <input value={this.state.name} onChange={this.handleChange} />
      </>
    );
  }
}
```

Now, define the `handleChange` event. Add it before the `render()` method in our class.

**App.js**

```
import React, { Component } from 'react';
import './style.css';

class App extends Component {
  constructor(props) {
    super(props);

    this.state = {
      name: '',
      displayName: ''
    };
  }

  handleChange = evt => {
    this.setState({
      name: evt.target.value
    });
  };

```

The handler function is a simple `arrow` function that accepts one argument, which is an event object React automatically passes in for you (also known as a synthetic event). You call it `evt` here, but you might see it called `e` or `event`.

In this function, update your `state`’s `name` value with whatever text your user has entered. To do that, use React’s built-in `state` updating method, `setState()`.

Call `setState()` and pass it an object that contains any `property:value` pair you want to update in `state`. You want to update the `name` property with a value of your text input which you can grab from the `evt` argument using `evt.target.value`.

#### Trigger a Greeting with a Button

For this to really be a true app, give your users a way to trigger a greeting message update after they’ve updated their name in the `input` box.

Add a button just under your `input` with a similar event handler, but this time the event will be `onClick` instead of `onChange`. You also give it some text, ‘`Update name`’. Also add the `handleClick` function for when the button is clicked.

**App.js**

```
 handleClick = evt => {
    this.setState({
      displayName: this.state.name
    });
  };

  render() {
    return (
      <>
        <h1>Welcome to the app</h1>
        <p>
          Hi there, {this.state.displayName}
        </p>
        <p>Enter your name below so we can get better acquainted</p>
        <input value={this.state.name} onChange={this.handleChange} />
        <button onClick={this.handleClick}>Update name</button>
      </>
    );
  }
}

export default App;
```

The `onClick` event is very similar to `onChange` and again it’ll receive a synthetic event argument you’ll just call `evt` again.

Your `click` handler method is doing the same update to `state` by calling the `setState()` method, but this time you’re updating your `displayName` value.

The `displayName` value is going to be the same as the final value they enter in the `input` box, which you already set to the `state` value, `name`. So that’s what you use to update `state` within your `handleClick` method.

### Test Your Greeting

Now that you have everything you need, save your `App.js` file, and take a peek in the browser. Enter a `name` in the `input` box and click ‘`Update name`’.

Instead of ‘`Hi there` ’, you get ‘Hi there, Vicki Bealman’ (or whatever name you entered).

#### Finishing touches

Save and take another look in the browser. It’s not an emmy award-winning app just yet, but you can see it looks a lot better already.

**App.js**

Last but not least, you have an initial message, ‘`Hi there`, ‘ and then just nothing. You make this a little more interesting by adding in a default message ’`we haven’t been introduced`’.

Do this by amending your initial greeting message using a logical `OR` statement. This sounds fancy, but it’s really a shorthand `if` statement in JavaScript you see used often in React to say ‘**evaluate both sides of this argument and return whichever is true**’.

**App.js**

**App.js**

```
render() {
    return (
      <>
        <h1>Welcome to the app</h1>
        <p>
          Hi there, {this.state.displayName || "we haven't been introduced"}
        </p>
        <p>Enter your name below so we can get better acquainted</p>
        <input value={this.state.name} onChange={this.handleChange} />
        <button onClick={this.handleClick}>Update name</button>
      </>
    );
  }
}

export default App;
```

Because your `state` value `this.state.displayName` is empty (`false`) by default, React will look at this and return the right-hand side of the argument, our default string.

**Congratulations**! Boom; that's it. That's your very first entrance into building a React app.

In the next section, you refactor your `App` component into smaller components and introduce some React Hooks.

***

#### Submit

Include the submit zip folder box here, with link to open code solution after submission.

***

#### Caution!

Be sure to zip up all of your documents to submit them
