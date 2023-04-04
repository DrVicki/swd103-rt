# L05HandsOn Project-Form Builder

### L05HandsOn Project-Form Builder

#### Requirements

1. Read the entire lesson, and code along with the guided learning to create the Form Builder App
2. Save your work frequently.
3. Copy the final URL to the completed project.
4. Paste URL in a text document.

For your project in this lesson, you create a Form Builder app. The Form Builder will allow you to dynamically create a number of form fields using a JSON file.

The final form will be assembled dynamically based on the JSON information and each form field's value will be captured in state.

You essentially build a really simplified version of the popular React form generators such as [Formik](https://formik.org/).

You can change the JSON file, adding and removing fields as you wish, and the form is automatically updated on the front end.

All the information from each field is captured and mock sent to your site owner via an email — this is what you’d like to do in real life, but for now, we’re just displaying the submitted form field values back to the user in a display box.

Start making your Form Builder.

#### Build the Form Builder

The Form Builder app is the most complex you've built so far. It builds on concepts from earlier lessons and reenforces the idea of building modular, component-driven UIs. You'll walk through the app step-by-step to create a dynamic form powered from a set of JSON objects.

Time to build something fun, the Form Builder app!

In this app, you will take a simple HTML form powered by React and allow it to load in a range of form fields dynamically from a JSON file.

It’s going to look like this when you’re done:

\


<figure><img src="https://github.com/DrVicki/swd103-rt/raw/main/Lesson-5/Lesson-5-Media/preview-formbuilder.png" alt=""><figcaption></figcaption></figure>

### Visualize the Components

Before you start building anything in code, however, it’s a great place to practice some of our ‘thinking in React’ skills.

As you get more experienced, you can code up what you need to and look at refactoring this as you go. In fact, it can be really helpful to rapidly and roughly build something out and just get it working and then concern yourself with refining it once it does.

But at this stage, it’s a super useful exercise to do a bit of planning beforehand to get a mental model and layout of what components you’ll need to build, and how they’ll interact.

#### Opportunities for breaking down components

Sticking with the finished demo you just looked at above, if you were to code this all up in one big component, it would look like this:

**LongFormExample.js (EXAMPLE ONLY**

```
function MyLongForm (props) {
  const [formValues, setFormValues] = useState({});

  const handleOnChange = e => {
    setFormValues({
      ...formValues,
      [e.target.name]: e.target.value
    });
  };

  const handleOnSubmit = () => {
    // do something when the form submits
  };

  return(
      <form onSubmit={handleOnSubmit}>
        <div className="field">
          <label className ="label">Name</label>
          <div className ="control">
            <input
                className ="input"
                type="text"
                placeholder="Annie Smith"
                onChange={handleOnChange}
                name="name"
                value={formValues['name']}
            />
          </div>
          <p className ="help">
            supply your first and last name
          </p>
        </div>
        <div className="field">
          <label className ="label">Password</label>
          <div className ="control">
            <input
                className ="input"
                type="password"
                onChange={handleOnChange}
                name="password"
                value={formValues['password']}
            />
          </div>
        </div>
        <div className="field">
          <label className ="label">Phone number</label>
          <div className ="control">
            <input
                className ="input"
                type="text"
                placeholder="+44 7809 12 34 56"
                onChange={handleOnChange}
                name="phone"
                value={formValues['phone']}
            />
          </div>
        </div>
        <div className="field">
          <label className ="label">Email</label>
          <div className ="control">
            <input
                className ="input"
                type="email"
                placeholder="annie@gmail.com"
                onChange={handleOnChange}
                name="email"
                value={formValues['email']}
            />
          </div>
          <p className ="help">
            email must be in the form 'user@domain.com'
          </p>
        </div>
        <div className="field">
          <label className ="label">Date of birth</label>
          <div className ="control">
            <input
                className ="input"
                type="date"
                onChange={handleOnChange}
                name="dob"
                value={formValues['dob']}
            />
          </div>
        </div>
        <div className="field">
          <label className ="label">Special message</label>
          <div className ="control">
            <input
                className ="input"
                type="text"
                onChange={handleOnChange}
                name="message"
                value={formValues['message']}
            />
          </div>
          <p className ="help">add any special instructions</p>
        </div>

        <button className="button is-primary">Sign up</button>
      </form>
  );
}
```

Ok, so this is already a really long component with much repetition, or very very close to having identical blocks of code — e.g. the label and input element combinations.

Granted, some of this additional markup is due to the styling imposed by Bulma, but even without that, you would still have many repeated blocks of code. This has a few disadvantages:

* Readability becomes more difficult as the file or component grows in size or complexity.
* Any universal changes (i.e. if you needed to change the styling or structure or logic) need to be made to each and every separate block rather than in one place.
* More repetition usually introduces more places for errors to occur.
* You also essentially ‘lock in’ this form and make it concrete. For example, we can’t reuse it anywhere, despite the fact that the mechanism of how it works (e.g. collecting data from the user and doing something with it) is going to be largely identical from form to form.

#### Create a Visual Map of Components

An improvement on this would be to look at the component you have and refactor it, thinking how you can maximize reuse and minimize errors and lines of code.

Thinking about the previous example and the previous demo of the app, you can create a visual mapping of how you might break down the single components into smaller parts.

<figure><img src="https://github.com/DrVicki/swd103-rt/raw/main/Lesson-5/Lesson-5-Media/l05-form-builder-components.png" alt=""><figcaption></figcaption></figure>

Looking at this visual mapping, you can see you have three main components and an additional file, `formfields.json`.

* `App.js` — The usual project entry point that defines the starting place for your app to begin.
* `Form.jsx` — This will be a container component that pulls in your JSON data from the `formfields.json` file and uses it to populate a dynamic list of `FormFieldInput` components.
* `FormFieldInput.jsx` — A semi-presentational component that renders an HTML input with a label, wrapped in a little bit of Bulma markup. It manages its own state for the input’s value.
* `formfields.json` — A simple JSON file that contains an array of objects, each representing a form field with some information like a name, label text, and input type.

### Project Setup

This part of the build should be starting to look familiar by now as you create a new project with Create React App, remove some default files you don’t need, and add Bulma’s CSS framework to the project.

Open a terminal window and navigate to the parent folder you want to create the new project in. Next, type the `create-react-app` command as follows:

****[**GET STARTER CODE HERE**](https://stackblitz.com/edit/react-kvqlbn?file=src/App.js)****

#### Initial Clean Up

After that, locate `/src/style.css` and delete the file.

Create the `/src/App.css` file.

Open the main `App.js` file located at `/src/App.js`.

Delete the `import style.css` file.

Now, select everything in the return statement (everything between return `()` and replace it with the following so the new return statement looks like this:

**App.js**

```
import React from "react";

export default function App() {
  return (
    <>
      <h1>Form Builder is ready to go</h1>
    </>
  );
}

```

<figure><img src="https://github.com/DrVicki/swd103-rt/raw/main/Lesson-5/Lesson-5-Media/form-builder-prev.png" alt=""><figcaption></figcaption></figure>

#### Add Bulma

The final stage in the setup is to, once more, bring Bulma onboard to help style your app.

* Add bulma to dependencies.

<figure><img src="https://github.com/DrVicki/swd103-rt/raw/main/Lesson-5/Lesson-5-Media/add-bulma.png" alt=""><figcaption></figcaption></figure>

Open up the file `/public/index.html` . If you remember, this is the template HTML file the project uses to render the initial output of the app.

Type `!` and enter to create boilerplate.

```
- Add `<div id="root"></div>`
```

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <div id="root"></div>
</body>
</html>
```

Next, add the following line somewhere between the opening and closing `<head></head>` tags:

`<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.0/css/bulma.min.css" />`

**index.html**

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <link
 rel="stylesheet"
 href="https://cdn.jsdelivr.net/npm/bulma@0.9.0/css/bulma.min.css"
/>

  <title>Document</title>
</head>
<body>
  <div id="root"></div>
</body>
</html>

```

<figure><img src="https://github.com/DrVicki/swd103-rt/raw/main/Lesson-5/Lesson-5-Media/meta-bulma.png" alt=""><figcaption></figcaption></figure>

You can also edit the title of the page between the `<title></title>` tags too if you like.

#### Project Structure

You’ve given some thought to the files you want and how you’re going to break the components down, but where are you going to house everything?

* Start by creating two **folders** directly underneath your `/src` folder: one will hold your components and one for your JSON data.
  * Create a new folder, `/components` and another one called `/data`.

<figure><img src="https://github.com/DrVicki/swd103-rt/raw/main/Lesson-5/Lesson-5-Media/file-structure.png" alt=""><figcaption></figcaption></figure>

When you start dealing with more complex projects and components that depend on each other, it can be helpful to start with the child furthest down the tree and build up from there.

* That’s how you’re going to build your components for the Form Builder. Starting with your JSON data, then you’ll look at the `FormFieldInput` component and build up (or backward, depending on how you look at it) from there.

This is helpful because it allows you to decide what information a child component will need ahead of time and then make sure you pass that down from the parent component when you’re building the parent out.

#### Create formfields.json

You want your HTML input elements to be rendered dynamically.

* This means they won’t know what to render ahead of time and will work this out at runtime, deciding which parts of the HTML to render, what type of field, etc.

This is good because it makes the component more flexible: want to render a simple text box? No problem. Want to use the exact same component to render a date picker instead that has some helper text? Fine and dandy.

However, at some point, you do have to let uour form field component know what you expect of it. A good way to do that is with some good, old fashioned structured JSON data.

Inside of the `/data` folder, create a new file called `formfields.json` and populate it with the following basic data:

**formfields.json**

```
{
  "fields": [
    {
      "label": "Name",
      "type": "input",
      "fieldName": "name",
      "placeholder": "Dr. Vicki",
      "helpText": "supply your first and last name",
      "required": true
    }
  ]
}
```

Thinking about the sort of properties your HTML input elements can have and the other sort of information you would like to have displayed by your form field input structure, you arrive at this structure.

* `label`; the text you want displayed in the `<label>` element.
* `type`; the value for the `type=“”` attribute on the input — this could be text, date, password, email, etc.
* `fieldName`; the name or id value for the field — this will be used in the `name=""` attribute.
* `placeholde`r; any text you want to have displayed initially in the input box.
* `helpText`; a convenience for your users which will display a little help message underneath the input.
* `required`; a boolean value that forces the user to enter some input.

You can make some of these optional, such as the help text and required values.

**The Complete formfields.json File**

Add a couple more fields to get a feel for how the rendered form fields will look in the end:

**formfields.json**

```
{
  "fields": [
    {
      "label": "Name",
      "type": "text",
      "fieldName": "name",
      "placeholder": "Dr. Vicki",
      "helpText": "supply your first and last name",
      "required": true
    },
    {
      "label": "Password",
      "type": "password",
      "fieldName": "password",
      "required": true
    },
    {
      "label": "Phone number",
      "type": "text",
      "fieldName": "phone",
      "placeholder": "+44 7809 12 34 56"
    }
  ]
}
```

Do you see where you left a couple of properties out of the password and phone number objects? You’ll discover how this affects the rendered output later on.

### Create the FormFieldInput Component

The first link in the chain is the `FormFieldInput` component. Create a new file, `FormFieldInput.jsx` in the `/components` folder.

Fill it with a basic structure before you build it out from there:

**FormFiledInput.jsx**

```
import React, { useState } from 'react';

const FormFieldInput = () => {
  return (
      <div className="field">
      </div>
  );
};

export default FormFieldInput;
```

#### Incoming Props

Next, define some props the `FormFieldInput` component will receive. These will be pretty much the same as those in the JSON file you just defined. Add them into the component using the JavaScript destructuring syntax we used previously:

**src/components/FormFieldInput.jsx**

```
import React, { useState } from 'react';

const FormFieldInput = ({
  label,
  type,
  fieldName,
  placeholder,
  helpText,
  required,
  handleFieldChange
}) => {
  
  return (
      <div className="field">
      </div>
  );
};

export default FormFieldInput;
```

You see they share the same name as the properties in the `JSON` file. This is useful as it means you can pass these directly from the `JSON` file into the component as you’ll see a little bit later on.

The only additional prop you need is the `handleFieldChange`. You use this as part of your input `onChange` event to inform the parent component your field’s value has changed.

#### Handle Input Changes

With your incoming props mapped out, set up your state and handle any changes on the input element.

**src/components/FormFieldInput.jsx**

```
import React, { useState } from 'react';

const FormFieldInput = ({
  label,
  type,
  fieldName,
  placeholder,
  helpText,
  required,
  handleFieldChange
}) => {

  const [value, setValue] = useState('');

  const handleOnInputChange = e => {
    setValue(e.target.value);

    if(handleFieldChange) {
      handleFieldChange(e.target.name, e.target.value);
    }
  };

  return (
      <div className="field">
      </div>
  );
};

export default FormFieldInput;
```

You use the `useState` Hook you imported at the top of the component to keep track of your input element’s value.

With the `handleOnInputChange` function, you capture the synthetic event, `e`, that React kindly provides. Use the value property like this, `e.target.value`, to update your state value using the `setValue` function returned from your Hook.

The next part is the interesting one. However many of these components you add onto the page, they each only track their own state and values. But when you’re thinking about form data, you’re thinking in terms of the overall form, not individual values. So how do you capture all the data from the form if you have multiple inputs but they’re just tracking single values?

* One way is to have the parent component (the one that renders all the individual input components) keep all the input values together in one place in its own state.

The way you’re going to handle this is have your child `FormFieldInput` component tell your parent component, `Form`, a value has changed using an event that Form passes down to us.

The prop `handleFieldChange` will be a function that accepts a field name and a field value. So here, you check that the function exists (you don’t want to call a function that hasn’t been passed in!) and if it does, call it passing in the synthetic event’s `e.target.name` and `e.target.value` values.

Don't worry about the mechanics of that function for now because ultimately, as a child component, you don’t care too much about what happens in your parent.

#### Define the JSX

The final part of the puzzle is to outline the HTML (or JSX) that will be rendered. Define that now and then walk through it:

**src/components/FormFieldInput.jsx**

```
  return (
      <div className="field">
        <label className="label">{label}</label>
        <div className="control">
          <input
            className="input"
            type={type}
            placeholder={placeholder}
            name={fieldName}
            value={value}
            onChange={handleOnInputChange}
            required={required || false}
          />
        </div>
        {
          helpText &&
          <p className="help">{helpText}</p>
        }
      </div>
  );
```

There’s nothing fancy in the `HTML` here, but it does have a few extra bits and pieces of structure to make the styling work. You can read more about the generic controls and inputs layout and styling directly in the Bulma CSS form [documentation](https://bulma.io/documentation/form/general/).

The key points here are to look at where you’re using your props. You’re defining a standard `HTML` input element and assigning props to the various input element’s attributes, such as `name` or `type`.

The input’s `value` attribute is using the `value` from state. This makes the input a controlled component from React’s point of view as it is managing the ‘state’ of the input’s value.

With `placeholder`, if that’s empty or null, then the input just won’t display anything, so that’s fine.

With `required`, you cater to a null value. If you pass `true` or `false`, that’s fine, because `required` will exist and have some boolean value. However, if it’s `null` or `empty` or `undefined` (or some other ‘falsey’ value) then this could cause issues. To cater to this, add a simple logical `OR` short circuit, the `required || false`.

You’ll become familiar with this as you look through React projects. It’s a common expression to find that essentially says ‘evaluate the first part of the expression and if it’s false, evaluate and return the second.

* So, if required is `null` or `undefined`, set the attribute to ‘`false`’.

You do a similar thing for the help text. Check to see if `helpText` is available. If it is, then check the section part of the expression after the `&&` and return it. This happens to be a JSX expression, which is also JavaScript, but it will get rendered out as a paragraph element containing your help text.

* This is a really handy and neat looking way to dictate if a portion of JSX is shown or not without complex `IF` statements or other complex mechanisms.

**The Complete FormFieldInput Component**

Here’s what the complete component should look like:

**src/components/FormFieldInput.jsx**

```
import React, { useState } from 'react';

const FormFieldInput = ({
  label,
  type,
  fieldName,
  placeholder,
  helpText,
  required,
  handleFieldChange
}) => {
  const [value, setValue] = useState('');

  const handleOnInputChange = e => {
    setValue(e.target.value);

    if(handleFieldChange) {
      handleFieldChange(e.target.name, e.target.value);
    }
  };

  return (
      <div className="field">
        <label className="label">{label}</label>
        <div className="control">
          <input
            className="input"
            type={type}
            placeholder={placeholder}
            name={fieldName}
            value={value}
            onChange={handleOnInputChange}
            required={required || false}
          />
        </div>
        {
          helpText &&
          <p className="help">{helpText}</p>
        }
      </div>
  );
};

export default FormFieldInput;
```

### Create the Form Component

The parent for your form fields is your `Form` component.

* Create that now by making a new file, `Form.jsx` in the `src/component` folder.

In terms of complexity, the `Form` component acts as a middle man of sorts. It collects and collates input changes from child input components, and then handles form submissions. Of course, it also renders the necessary `HTML` form elements including a default submit button.

Scaffold out the basic component first:

**Form.jsx**

```
import React, {useState} from 'react';

// components
import FormFieldInput from './FormFieldInput';

const Form = () => {
  return (
    <form onSubmit={onFormSubmit}>
		// Form fields here
      <div className="control">
        <button className="button is-primary">Sign up</button>
      </div>
    </form>
  );
};

export default Form;
```

Nice and simple to start with. Import `React` and `useState` from React. Then bring in your `FormFieldInput` component and define a `Form` component.

As part of the initial JSX returned, you use a standard `HTML` form element with a React event `onSubmit` handled by the `onFormSubmit` function you’ll define in a moment.

Add a default `button` element with some Bulma wrapping and classes for styling purposes.

* The `button` doesn’t wire up to any event handling, but by default, when a `button` element exists within a form element, when it is clicked it triggers the form’s `onSubmit` event.

#### Incoming Props

You have two props to outline here; `handleFormSubmit` and `formFields`.

* The former is a function called when you handle your form’s `onSubmit` event. Similar to the way the `FormFieldInput` handles its input value changes and then calls an event passed in by the parent, your `Form` component is going to do the same with `handleFormSubmit`.
* The latter, `formFields` will be an array of form field data objects you’ll loop through and use to render a separate `FormFieldInput` component.

**src/components/Form.jsx**

```
import React, {useState} from 'react';

// components
import FormFieldInput from './FormFieldInput';

const Form = ({
  handleFormSubmit,
  formFields,
}) => {
  
  return (
    <form onSubmit={onFormSubmit}>
		// Form fields here
      <div className="control">
        <button className="button is-primary">Sign up</button>
      </div>
    </form>
  );
};

export default Form;
```

#### Handle form Submissions and input Changes

You have your props defined. Outline some variables and event handlers:

**src/components/Form.jsx**

```
import React, {useState} from 'react';

// components
import FormFieldInput from './FormFieldInput';

const Form = ({
  handleFormSubmit,
  formFields,
}) => {

  const [formValues, setFormValues] = useState({});

  const handleFormValuesChange = (name, value) => {
    setFormValues({
      ...formValues,
      [name]: value
    });
  };

  const onFormSubmit = e => {
    e.preventDefault();
    if(handleFormSubmit) {
      handleFormSubmit(formValues);
    }
  }

  return (
    <form onSubmit={onFormSubmit}>
		// Form fields here
      <div className="control">
        <button className="button is-primary">Sign up</button>
      </div>
    </form>
  );
};

export default Form;
```

The `formValues` variable uses the familiar `useState` Hook and you use it to add or update any new form field values as they change.

The `handleFormValuesChange` function is what you pass down to any and all child `FormFieldInput` components. It’ll be fired on each input change in the child component and its sole job is to take the updated value and add or amend it in your local `formValues` state object.

Similarly, the `onFormSubmit` function does a simple, singular task. After preventing the form from causing a full page refresh using `e.preventDefault()`, it checks to see if the props function `handleFormSubmit` is available. If so, it calls it, passing up the current state of `formValues`.

In your case, the parent component here will be `App` and you look at what you do with the `formValues` it receives shortly when you build that component out.

### Define the JSX

All that’s left to do now is add a number of `FormFieldInput` components into the body of your `Form` component.

Leaving the majority of the current JSX you defined intact, **replace the commented section**, `//` Form fields here with the following code:

**src/components/Form.jsx**

```
      {
        formFields.map(fieldDetails =>
            <FormFieldInput
              key={fieldDetails.fieldName}
              handleFieldChange={handleFormValuesChange}
              {...fieldDetails}
            />
        )
      }
```

Your `formFields` prop is an array of objects, each containing a set of form field properties. You’re using the `.map()` function on the array to loop through and return a new array full of JSX markup; in this case, each item in the `formFields` array will return a new `FormFieldInput` component.

You add a key attribute, which is vital when producing output in a loop. This is what React uses to keep track of changes in repeated sections of JSX. Then add in the `handleFormValuesChange` function to the attribute `handleFieldChange` so that it’s passed into the child component.

#### Destructure prop Attributes

The next bit might look a little strange. Take a look at the `{…fieldDetails}` line. You might recognize the `...` syntax as the object destructuring syntax built into newer versions of JavaScript.

However, you use it here as shorthand instead of typing out each individual property on the `FormFieldInput` component.

You’ll remember from when we defined the component that it expects the following props:

* `label`
* `type`
* `fieldName`
* `placeholder`
* `helpText`
* `required`
* `handleFieldChange`

With the exception of `handleFieldChange` all the other props are named identically to the object properties on \`one of our form field JSON objects.

What this means is that by saying `{…fieldDetails}` on the component, you’re really saying, ‘please copy all the properties and values from the `fieldDetails` object (which represents a single item in the `formFields` array) onto our `FormFieldInput` component.

Let’s quickly highlight this with a code example:

**Just an Example-Don't Use**

```
// in the loop
{
	formFields.map(fieldDetails =>
		// this VVV  	
		<FormFieldInput
         {...fieldDetails}
        />

		// is exactly the same as doing this
		<FormFieldInput
          label={fieldDetails.label}
          type={fieldDetails.type}
          fieldName={fieldDetails.fieldName}
          placeholder={fieldDetails.placeholder}
          helpText={fieldDetails.helpText}
          required={fieldDetails.required}
        />
   )
}
```

Although the second version is more explicit in that you know exactly what’s being passed from into the `FormFieldInput`, the first version is much neater and serves the same purpose. It would be much more fitting if it were part of a larger, more complex component that we could refactor to make more readable.

**The Complete Form Component**

Here’s what the complete component should look like:

**src/components/Form.jsx**

```
import React, {useState} from 'react';

// components
import FormFieldInput from './FormFieldInput';

const Form = ({
  handleFormSubmit,
  formFields,
}) => {
  const [formValues, setFormValues] = useState({});

  const handleFormValuesChange = (name, value) => {
    setFormValues({
      ...formValues,
      [name]: value
    });
  };

  const onFormSubmit = e => {
    e.preventDefault();
    if(handleFormSubmit) {
      handleFormSubmit(formValues);
    }
  }

  return (
    <form onSubmit={onFormSubmit}>
      {
        formFields.map(fieldDetails =>
            <FormFieldInput
              key={fieldDetails.fieldName}
              handleFieldChange={handleFormValuesChange}
              {...fieldDetails}
            />
        )
      }
      <div className="control">
        <button className="button is-primary">Sign up</button>
      </div>
    </form>
  );
};

export default Form;
```

### Edit App.js

With all the building blocks in place, the last thing to do is wire everything up into your starting point, the `App` component.

Open the `App.js` component in the project root. Add some imports first:

**src/App.js**

```
import React, { useState } from 'react';

// components
import Form from './components/Form';

// data
import data from './data/formfields.json';

export default function App() {
  return (
    <>
      <h1>Form Builder is ready to go</h1>
    </>
  );
}
```

You bring in both the `Form` component and the `JSON` data from the `formfields.json` file.

Next, inside of the `App` functional component, use `useState` to set up a place to house the collected form values when the HTML form is submitted.

We now add `export default App;`.

**src/App.js**

```
import React, { useState } from 'react';

// components
import Form from './components/Form';

// data
import data from './data/formfields.json';

function App() {
  const [submittedFormValues, setSubmittedFormValues] = useState([]);

  return (
    <>
      <h1>Form Builder is ready to go</h1>
    </>
  );
}

export default App;
```

And finally, add in the `JSX`. First, add in the structural elements infused with the Bulma styles.

**src/App.js**

```
return (
    <div className="section">
      <div className="container">
        <h1 className="title is-size-2">Form Builder</h1>
        <hr />
        <div className="columns">
          <div className="column">
            <h2 className="title is-size-4">Sign up for an account</h2>
            <div className="box">

					// We'll add our form here

            </div>
          </div>
          <div className="column is-offset-1">
            <div className="content">
              <h2 className="title is-size-4">Form results</h2>
              <p>Form results will be submitted here each time you click the 'sign up' button</p>
              <div className="notification">

					// We'll output the collected form values here

              </div>
              <button 
					className="button is-light" 
					onClick={() => setSubmittedFormValues({})}
				  >
                clear results
              </button>
            </div>
          </div>
        </div>
     </div>
    </div>
);

```

<figure><img src="https://github.com/DrVicki/swd103-rt/raw/main/Lesson-5/Lesson-5-Media/preview-formbuilder.png" alt=""><figcaption></figcaption></figure>

Everything so far should look pretty straightforward. Bulma, like most CSS frameworks, dictates a lot of additional styles and some additional markup to layout and style everything according to its own approach.

* Here, you add a `section`, `container`, `title` and some columns which Bulma bases on the flexbox CSS model. The box class will give your form a nice surrounding border and box-shadow.

Meanwhile, on the other side, the `notification` class will highlight your eventually outputted form values with a background and some spacing.

The only other thing for now is you have a ‘clear results’ `button` that calls the `setSubmittedValues()` method to reset the value in state, effectively clearing out the results you'’ll display in a moment.

Output some of the form values you can expect to receive when the form is submitted:

**src/App.js**

```
   return (
    <div className="section">
      <div className="container">
        <h1 className="title is-size-2">Form Builder</h1>
        <hr />
        <div className="columns">
          <div className="column">
            <h2 className="title is-size-4">Sign up for an account</h2>
            <div className="box">

					// We'll add our form here

            </div>
          </div>
          <div className="column is-offset-1">
            <div className="content">
              <h2 className="title is-size-4">Form results</h2>
              <p>Form results will be submitted here each time you click the 'sign up' button</p>
              <div className="notification">
              {
                  Object.values(submittedFormValues).length <= 0 &&
                      <p>Submit a form to see the results</p>
                }
                <ul>
                {
                  Object.entries(submittedFormValues).map(([key, value]) => (
                      <li key={key}>{value}</li>
                  ))
                }
                </ul>
              </div>
              
              <button 
					className="button is-light" 
					onClick={() => setSubmittedFormValues({})}
				  >
                clear results
              </button>
            </div>
          </div>
        </div>
     </div>
    </div>
);
}

export default App;
```

The first code block uses the logical `AND` shortcut to check if the `submittedFormValues` object in state has any values. Use JavaScript’s `Object.values()` for this job.

* You can read the [MDN developer documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_objects/Object/values) on this for more information.

If the object in state doesn’t have any values, it’s an empty object, so check the other side of the expression. The right hand side happens to be a paragraph tag informing the user they need to submit the form to see some results.

Next, define a standard unordered list and do a similar statement as you’ve just done. This time you look through each `key:value` pair in the `submittedFormValues` object using JavaScript’s `Object.entries()`.

* Again, here’s some great documentation on the [MDN developer site](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Object/entries).

Each item in the loop gives both a key and a value for each property in the object in state. For each `key:pair` value, you return (and render) an HTML list item element that contains this pair’s value. For example, if the current object property was `name: ‘Rob Kendal'` then you’re just be grabbing ’`Rob Kendal`’.

Finally, add the `Form` component.

**src/App.js**

```
              return (
    <div className="section">
      <div className="container">
        <h1 className="title is-size-2">Form Builder</h1>
        <hr />
        <div className="columns">
          <div className="column">
            <h2 className="title is-size-4">Sign up for an account</h2>
            <div className="box">

            <Form
                handleFormSubmit={values => setSubmittedFormValues(values)}
                formFields={data.fields}
              />

            </div>
          </div>
          <div className="column is-offset-1">
            <div className="content">
              <h2 className="title is-size-4">Form results</h2>
              <p>Form results will be submitted here each time you click the 'sign up' button</p>
              <div className="notification">
              {
                  Object.values(submittedFormValues).length <= 0 &&
                      <p>Submit a form to see the results</p>
                }
                <ul>
                {
                  Object.entries(submittedFormValues).map(([key, value]) => (
                      <li key={key}>{value}</li>
                  ))
                }
                </ul>
              </div>

              <button 
					className="button is-light" 
					onClick={() => setSubmittedFormValues({})}
				  >
                clear results
              </button>
            </div>
          </div>
        </div>
     </div>
    </div>
);
}

export default App;
```

Simple, right? you already completed all the hard work by defining and building out components. Now you have the relaxing job of just adding in the component. The only remaining thing is to wire up the `Form` component’s props, namely the `handleFormSubmit` event and the `formFields`. You passed along the fields array from your JSON file into the `formFields` prop.

With the `handleFormSubmit` prop, you run an inline arrow function that receives a values object containing the form field names and their values, and immediately call the `setSubmittedFormValues` to update these names in state.

As soon as the value of `submittedFormValues` in state changes, the component will render again, and your notification area will be populated (assuming of course that submittedFormValues contains any values!).

**The Complete App Component**

Here’s what the complete component should look like:

**src/App.js>**

```
import React, { useState } from 'react';

// components
import Form from './components/Form';

// data
import data from './data/formfields.json';


function App() {
  const [submittedFormValues, setSubmittedFormValues] = useState([]);

  return (
    <div className="section">
      <div className="container">
        <h1 className="title is-size-2">Form Builder</h1>
        <hr />
        <div className="columns">
          <div className="column">
            <h2 className="title is-size-4">Sign up for an account</h2>
            <div className="box">
              <Form
                handleFormSubmit={values => setSubmittedFormValues(values)}
                formFields={data.fields}
              />
            </div>
          </div>
          <div className="column is-offset-1">
            <div className="content">
              <h2 className="title is-size-4">Form results</h2>
              <p>Form results will be submitted here each time you click the 'sign up' button</p>
              <div className="notification">
                {
                  Object.values(submittedFormValues).length <= 0 &&
                      <p>Submit a form to see the results</p>
                }
                <ul>
                {
                  Object.entries(submittedFormValues).map(([key, value]) => (
                      <li key={key}>{value}</li>
                  ))
                }
                </ul>
              </div>
              <button className="button is-light" onClick={() => setSubmittedFormValues({})}>
                clear results
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  );
}

export default App;

```

<figure><img src="https://github.com/DrVicki/swd103-rt/raw/main/Lesson-5/Lesson-5-Media/final-appjs.png" alt=""><figcaption></figcaption></figure>

### View the Project

So, all that’s left to do is marvel at your handiwork. This might look like a fairly simple project on the surface, but it is deceptively deep when you get into it.

* You abstracted much repeated code into reusable, independent components that each manage their own state.
* You employed some structured JSON data to dynamically dictate what types of form fields to render.
* You started to think in React to achieve all this, passing values and information down through props, and back up via events and handler functions.

Enter some data into the form, check out the built in HTML validation in play on the required fields, and try submitting the form. Notice how the notification display updates with whatever you enter in the form? Pretty cool, right?

#### Change the JSON Data

Now for the real magic. The power of your dynamically generated form really shines through if you change any of JSON data in the `formfields.json` file. Do that now and check out the results.

* Add a new `field` and change some details on the others. As soon as you hit save on the file, watch the form in the local site update to reflect those changes. If you submit the form again, notice how the correct data is being pulled together and displayed in the notification area.

Now that’s really cool and so powerful for two components and not that many lines of code!

**Optional Challenge**

You built something very useful here that offers a lot of flexibility and power in such a small package. There are many ways to extend it which offer some challenges and you can take and experiment with.

For example, you could:

1. Look at adding in dynamic validation to the form field components.
2. Add different types of HTML form elements, such as selects, text areas, or sliders.
3. Add some moving parts to the Form component such as notifications on submission, call back functions, and introductory messaging.

**Submission**

1. Zip text document
2. Upload Zip folder
