---
title: "React | 💙"
permalink: /dev/03-deliverable-react
layout: default
---

# React.js Deliverable

### Creating a To-Do List App

For this deliverable, you will be creating an app with to-do list functionalities, including adding to-do items, crossing them off, and keeping track of how many items are in your to-do list at any point in time.

### File setup

In your command line or terminal:

```shell
create-react-app todo-list
```

This will create a new React project in a folder called “todo-list.” If this command doesn’t work, make sure you have Node >= 10.16 and npm >= 5.6 on your machine. Once the create-react-app command is done running, cd into your project folder and type “code .” to open your project in VSCode.

```shell
cd todo-list
code .
```

There will be a lot of boilerplate code in your new project. Delete **app.test.js**, **setupTests.js**, and **logo.svg** from src– we won’t be using them.

Now, let’s look at **app.js**, where the bulk of our code will be added. Notice that the return statement has an HTML-like syntax. This syntax expression is called JSX and is a shorthand way of writing out a tree of HTML elements.

React is using JSX to construct a DOM, or document object model. A DOM is the underlying tree of HTML elements that make up a document.

Start by deleting the default page elements in the header component and replacing it with the title of our app. In other words, modify **app.js** so that it becomes:

```react
 import React from "react";
 import "./App.css";

 function App() {
    return (
        <div className = "App">
            <header className = "App-header">
                <p>React Todo</p>
            </header>
        </div>
    );
 }

 export default App;
```

Let’s begin to define some **states** in our App component. States are objects or data types that contain information for our component. React uses states to determine how the component behaves. A React state is immutable and cannot be modified.

In App.js, we will define a single piece of state called Todos which will be an array.We will use a hook called **useState**. Add the following two lines:

`import {useState} from "react";` and `*const*[todos,setTodos] = useState([]);`.

```react
import {useState} from "react";
import "./App.css";

function App() {

    const[todos,setTodos] = useState([]);

    return (
        <div className = "App">
            <header className = "App-header">
                <p>React Todo</p>
            </header>
        </div>
    );
 }

 export default App;
```

Our app will consist of three main components:

- **TodoForm.js** : keeps track of our todo state through a form

- **TodoList.js** : renders a list of todos

- **Todo.js** : renders a todo object and handles its objects

Create a **components** folder in **src**. Create these three files in this folder. This folder stores all the components, or pieces, of our React program. For example, in a Twitter program, the feed, tweets, sidebar, and user items are likely all components. Components have their own structure and are reusable.

Set up **TodoForm.js** by importing React, creating a **TodoForm()** function, and exporting that function as a default. In the function, return a form element with an input and a button inside of it.

We also need to define some state to keep track of input from the user. At the top of TodoForm.js, define a state called **todo** with **setTodo** as the function, initialized as an object with three properties: **ID** (string), **task** (string), **completed** (boolean).

```react
 import { Button} from "@material-ui/core";
 import { useState } from "react";
 
 function TodoForm() {
  const[todo, setTodo] = useState({
    id: "",
    task: "",
    completed: false
  });
 
  return(
    <form>
      <input />
      <button />
    </form>
  );
 }
 
 export default TodoForm;
```

