# L07HandsOnAssignment

### L07HandsOnAssignment

Look at what you’ll be building:

<figure><img src="https://github.com/DrVicki/swd103-rt/raw/main/Lesson-7/Lesson-7-Media/l07preview.png" alt=""><figcaption></figcaption></figure>

#### Requirements

1. Follow guided learning
2. Copy URL to completed Project
3. Put URL on text document

****[**Lesson 7 HandsOn Assignment Starter Code**](https://stackblitz.com/edit/react-zvkunf?file=src/App.js)****

1. Fork the repository
2. Name it L07HandsOnAssognment

#### Why Routing?

Routing refers to keeping a webpage up to date with the current URL, and vice-versa.

Most of the apps you’ve written so far have been single-page applications. One HTML page whose content is updated through user interactions and JS. These DO NOT use routing.They work fine, but put some limits on the user experience of our applications.

**Question: What are some advantages routing can provide?**

<details>

<summary>Click her for answers></summary>

1. Users can use URLs to bookmark pages
2. Users can use the back or forward button
3. Users can easily share content from a page in the app

</details>

If you have written a multi-page application, you may have wrestled with Webpack configs in order to get all your pages built successfully. Fortunately, routing with React is easier than managing Webpack configuration! We just need to use a library called [React Router](https://v5.reactrouter.com/web/guides/quick-start).

#### The Code

Rather than tell you about how Router works, we’ll work through a brief example.

We’ll be using tthe starter code.

#### Getting Started

1. Create a `components` folder inside the `src` folder.

`src/components`

2. Create a `Home.js` folder in the `components` folder

Add the followimng code to `Home.js`

```
import React from "react";
 
const Home = () => {
  return <div>Home Page</div>;
};
 
export default Home;
```

3. Create `About.js` in `componsnts`.

Add the following code.

```
import React from "react";
 
const About = () => {
  return <div>About page</div>;
};
 
export default About;
```

4. Create `Contact.js` in `components`

Add the following code.

```
import React from "react";
 
const Contact = () => {
  return <div>Contact Page</div>;
};
 
export default Contact;
```

In all the above `components` we created a functional component that returns a `div` containing the name of the page.

* You can also add other content to these pages but right now we have kept the components simple to show the use of routers in react.

Now your project directory will have the following structure.



**NOTE**

You will see minor errors pop up in the preview while we wire everything together.

* This is normal.
* I will indicate with an image when there should actually be a functional preview and no errors.

#### Installing React Router

There are three different packages for routing in React. These are :

* `react-router` : It gives the React Router apps with the core routing methods and components.
* `react-router-native` : It is used in building apps for android and ios.

react-router-dom\` : Web designing utilities are contained by it.

`react-router` cannot be directly used in your application. To utilise `react routing`, you must first install the `react-router-dom` dependency and components in your application.

1. Add react-router-dom in "Dependencies"
2. Add react-router in "Dependencies"

#### Components in React Router

The router component :

* `BrowserRouter` : It allows the handling of a dynamic URL. The HTML5 history API (`pushState`, `replaceState` and the `popstate` event) is used to synchronise the API with the URL.

The browser router takes the following four attributes :

* `basename`: **string** The fixed or base URL for all locations. If your app is served from a sub directory on your server, set this to that directory. A properly constructed `basename` should begin with a slash and end without any slash.

```
//Example only

<BrowserRouter basename="/user">
    <Link to="/profile"/> // renders <a href="/user/profile">
    <Link to="/about"/> // renders <a href="/user/about">
    ...
</BrowserRouter>
```

* `getUserConfirmation`: **func** A function used to confirm navigation. Defaults to using window.confirm.

```
//Example Only

<BrowserRouter
  getUserConfirmation={(message, callback) => {
    // this is the default behavior
    const allowTransition = window.confirm(message);
    callback(allowTransition);
  }}
/>
```

* `forceRefresh`: **bool** If true, the router will perform complete page refreshes while navigating between pages. You might use this to mimic the behaviour of a standard server-rendered app, with full page refreshes between page navigation.

```
//Example only

<BrowserRouter forceRefresh={true} />
```

* `keyLength`: **number** The length of location.key. Its default value is 6.

```
//Example only

<BrowserRouter keyLength={12} />
```

#### Adding Routes

Now, after installing the `react-router-dom` you can now add a `router` in the react app.

We will be making use of the `browserRouter`. Now the browser router must wrap all the components of the application. To wrap all elements, you can either make it the parent element in the `App.js` file or simply use `App.js` inside the `BrowserRouter` in the i`ndex.js` file.

In the `index.js` file, make the following changes :

```
//index.js

import React from "react";
import ReactDOM from "react-dom/client";
import "./index.css";
import App from "./App";
import { BrowserRouter as Router } from "react-router-dom";
 
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <Router>
    <App />
  </Router>
);
```

In the above code, the `BrowserRouter` has been imported as `Router`. The `App` has been wrapped in the `Router` to facilitate the routing of the whole application.

Now to finally start adding Routes in your application, open the `App.js` file and import `Routes` and `Route` from `react-router-dom`.

Have a look at what these terms mean :

* `Routes` - When the location changes, `Routes` searches through all of its child routes for the best match and renders that branch of the UI. Nesting of Route components may be done to show nested UI, which also corresponds to nested URL paths. Parent routes render their child routes on the basis of these nested routes.
* `Route` - A single `route` is created with the help of Route. It takes in two attributes :
  * `Path` - It is used to specify the path of the URL for which the current element must be shown. You can call this pathname whatever you want. Also, the first pathname is a backslash `(/)`and is always used first. When the app loads for the first time, any component with a backslash in its pathname gets displayed first. This means that to make the `Home` component to be present in our application first we need to use the backslash path with it.
  * `element` - This specifies what component must be rendered for a specific route.

Now to use these in your application, first import all the components you had created in the `components` directory.

So now your code in `App.js` file must look like the following :

```
//App.js

import React from 'react';
import { Routes, Route } from "react-router-dom";
import About from "./components/about";
import Home from "./components/Home";
import Contact from "./components/contact";
import "./App.css";
 
function App() {
  return <div className="App"></div>;
}
 
export default App;
```

**Will see errors-don't worry**

We have removed all the default code from the `app` component.

Now you need to define the routes and attach the respective components.

```
//App.js

import React from 'react';
import { Routes, Route } from "react-router-dom";
import About from "./components/about";
import Home from "./components/Home";
import Contact from "./components/contact";
import "./App.css";
 
function App() {
  return (
    <div className="App">
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>
    </div>
  );
}
 
export default App;
```

**May see errors-don't worry**

The `/` path is attached to the `Home` component so it will show up first. The `/about` url path will give the `About` page and the `/contac`t url path will give the `Contact` component.

This way you have defined the routes in your application.

#### Basic Routing

Now you have defined the routes. It is time for you to connect these components to each other. The `react-router-dom` components `<Link>` and `<NavLink>` are used to navigate throughout the react application. While navigating, we often employ anchor tags for this reason.

Anchor tags cause the page to refresh and re-render all of its components. In contrast, `<Link>` and `<NavLink>` will only re-render updated components that match the Route's URL route without reloading. It allows Single-Page Applications to route more quickly.

**"Link" Component Props** :

* `to` : String or object which specifies the pathname.
* `replace` : Replaces the pathname in the history stack with new.
* `innerRef` : Passes ref to the element rendered by the component.

**"NavLink" Component Props** :

* `className` : Specifies the CSS class name you want to apply to the element when active.
* `isActive` : Returns boolean value whether the link is active or not.
* `style` : To apply inline CSS.
* `end` : Match the pathname precisely with the URL.
* `to`, replace, innerRef same as the Link Component.

A special kind of `<Link>` is `<NavLink>` has the information about itself being active or not. It is also used to apply styling to the Link.

**Now add the Link component** in the home page. We will add the links in the `Home` component so all the pages can be visited from the home page.

```
//Home.js

import React from "react";
 
const Home = () => {
  return (
    <div>
      <Link to="about">Click to view our about page</Link>
      <Link to="contact">Click to view our contact page</Link>
      <p>Home page</p>
    </div>
  );
};
 
export default Home;
```

In above code two links have been created to the about and contact page.

#### Nesting Routes

`Routes` might expand and get more complicated. Nested routes are used by **React Router** to provide more specific routing information within child components.

Now to understand the nesting of routes, **create a user route and a user component**.

* Create two components: `user profile` and `user account`. These two will be nested in the user route.

So create two new components with the name UserProfile.js and UserAccount.js.

**User Profile**

```
//UserProfile.js

import React from "react";
 
const UserProfile = () => {
  return <div>User Profile</div>;
};
 
export default UserProfile;
```

**User Account**

```
//UserAccount.js

import React from "react";
 
const UserAccount = () => {
  return <div>User Account</div>;
};
 
export default UserAccount;
```

Now you need to define a `User` component in which you will be doing nested routing. So create a new component `User.js` with the following code :

```
//User.js

import React from "react";
import { Routes, Route } from "react-router-dom";
import UserAccount from "./UserAccount";
import UserProfile from "./UserProfile";
 
const User = () => {
  return (
    <div>
      <p>User</p>
      <Routes>
        <Route path="/profile" element={<UserProfile />} />
        <Route path="/account" element={<UserAccount />} />
      </Routes>
    </div>
  );
};
 
export default User;
```

In the above code, under the `Routes`, two routes have been defined, one for the `/profile` and one for the `/account` . The `UserProfile` and `UserAccount` components have been imported. The `/profile` is attached to the `UserProfile` component, and the `/account` is attached to the `UserAccount` component.

Now you need to route from the main app to the `User` component. Then only the `User` component and its nested routes will work. So add the route for the `User` component in the `App.js` file as shown:

```
//App.js

impoert React from 'react';
import { Routes, Route } from "react-router-dom";
import About from "./components/About";
import Home from "./components/Home";
import Contact from "./components/Contact";
import "./App.css";
import User from "./components/User";
 
function App() {
  return (
    <div className="App">
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="about" element={<About />} />
        <Route path="contact" element={<Contact />} />
        <Route path="user/*" element={<User />} />
      </Routes>
    </div>
  );
}
 
export default App;
```

You must have noticed the path for the user component is different from the rest of the routes.

* The path `user/*` means for any path starting with `user/`, the `User` component will be rendered. In other words, if you type `/user/random` or `/user/lorem` or anything like this, the `User` component will be rendered.

Now we wanted the `/user/profile` path to give us the `UserProfile` component and the `/user/account` path to give us the `UserAccount` component. So if the user enters `/user/profile`, the `User` component will be rendered, and in the user component, the routing for the rest of the path, that is `/profile` will be done and the `UserProfile` component will be rendered. The same will be the case for the `/user/account` path, the `UserAccount` component will be rendered.

Now the final task left is to add links for the `UserProfile` and `UserAccount` components. So add the two links in the `Home.js` file as shown:

```
//Home.js

import React from "react";
import { Link } from "react-router-dom";
 
const Home = () => {
  return (
    <div>
      <p>
        <Link to="about">Click to view our about page</Link>
      </p>
      <p>
        <Link to="contact">Click to view our contact page</Link>
      </p>
      <p>
        <Link to="/user/profile">Click to view our user profile page</Link>
      </p>
      <p>
        <Link to="/user/account">Click to view our user account page</Link>
      </p>
      <p>Home page</p>
    </div>
  );
};
 
export default Home;
```

### BOOM!

You should now have all routes wired up, and see this beautiful rendering.

<figure><img src="https://github.com/DrVicki/swd103-rt/raw/main/Lesson-7/Lesson-7-Media/l07preview.png" alt=""><figcaption></figcaption></figure>

It's not fancy, but it demonstrated how to use Routing in React.

You can add content to each page if you want to.

**Submission**

1. Zip the text document with project URL
2. Upload folder
