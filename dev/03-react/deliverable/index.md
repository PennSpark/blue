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

Now, we need to define a function within TodoForm() to handle when the user types an input for a todo so we can keep track of it in our state. **Let’s call this function handleTaskInputChange()**. It takes in an event **e** as a parameter and is responsible for updating the task property from above.

```react
function handleTaskInputChange(e) {
    setTodo({...todo, task:e.target.value});
}
```

Moving down to our return statement, we need to define the **onChange** function to run the handleTaskInputChange function every time the event is fired (when the input changes). We also need to set the value of the input to the todo’s task because that’s what is being updated. 

Modify the return statement like so: 

```react
 return(
    <form>
      <input
        name = "task"
        type = "text"
        value = {todo.task}
        onChange = {handleTaskInputChange}
      />
      <Button type="submit">Submit</Button>
    </form>
  );
```

Now, we need to handle the case of adding a new todo to the list.Return to **App.js** and create a function called **addTodo()** that will take in a todo and add it to the array of todos. 

In order to add the new todo, we need to create a new todos array by calling the setTodos array and combining the new todos with the existing one. In **App()**, add: 

```react
function addTodo(todo) {
    setTodos([todo, ...todos]);
}
```



At the top of **App.js**, add: 

```react
import TodoForm from "./components/TodoForm";
```



In the return header, add:

```react
<TodoForm addTodo={addTodo}/>
```



In **TodoForm.js**, we need to destructure the addTodo function from the props parameter.

```react
function TodoForm({ addTodo }) {
```



When the user submits the form, we want to add the form’s todo from the state to the list of todos. In order to do this, we need to create a **HandleSubmit** function that takes an event. 

Here, we need to call the preventDefault function to prevent default submit form functionality. Then, we will write an if-statement that only gets called if a todo’s task is not empty by calling the trim function which removes a string’s white space. Inside the if-statement, call the new addTodo function with an object that has the todo and an updated ID property. 

This ID comes from a package called uuid. To install it, open the terminal and enter: 

```shell
yarn add uuid 
```

Then, import uuid and call v4 to generate the id. The import statement at the top of TodoForm.js looks like: 

```react
import uuid from "uuid";
```

We also want to reset the form that has updated new properties. We can use setTodo. 

When complete, the handleSubmit function should look like: 

```react
function handleSubmit(e) {
    e.preventDefault();
    if (todo.task.trim()) {
      addTodo({ ...todo, id: uuid.v4() });
      setTodo({ ...todo, task: "" });
    }
  }
```

In the return statement, define the form’s onSubmit property to be the new handleSubmit property. Make the following line modification in TodoForm.js: 

```react
<form onSubmit={handleSubmit}>
```

Now, we will switch gears and work in **TodoList.js**. Start by importing React, creating a **TodoList()** function, and exporting it as a default. 

From the component’s props, destructure todos (add `{ todos }` as a parameter ).

We also want to return an unordered list of todos by using the .map() array function. Inside of the map, return the Todo component by returning the Todo object as a prop. When rendering an element from an array map, each element should have a unique key. 

The finished TodoList.js looks like: 

```react
import React, {useState} from "react";
 import Todo from "./Todo";
 
 function TodoList({ todos }) {
    return(
        <ul>
            {todos.map(todo => (
                <Todo />
            ))}
        </ul>
    );
 }
 export default TodoList;
```

Now, let’s define what a Todo will look like. It should have a checkbox, a task, and a delete element. Move to **Todo.js**. 

Set up the file in the same way. (Import React, write Todo() with return(), and export it as a default.)

In the return statement, create an input (checkbox), a list item with the task, and an X button. However, we cannot return multiple elements at once from a React component. We must wrap these elements in a div element, which I can also use to align the elements. 

Speaking of aesthetics, we can use CSS to attribute style elements. I will assign completed items to have red strikethroughs. 

```react
import React from "react";
 
function Todo({ todo }) {
    return (
        <div style = {{display: "flex"}}>
            <input type = "checkbox" />
            <li
                style = {{
                    color: "white",
                    textDecoration: todo.completed ? "line-through" : null
                }}
            >
                {todo.task}</li>
            <button>X</button>
        </div>
 
    );
}
export default Todo;
```

Remember to import the function in **App.js**: 

```react
import TodoList from "./components/TodoList";
```

And to use it in App’s return statement: 

```react
<header className = "App-header">
  <p>React Todo</p>
  <TodoForm addTodo={addTodo}/>
  <TodoList todos={todos} />
</header>
```



Next, we need to implement actions that can be performed on the todos: toggle complete and delete. 

Navigate back to **App.js** and make a new function called **toggleComplete** which takes in the ID of the todo. In the function, call setTodos and pass a new array that is obtained by mapping. We intend to iterate through the array and find the todo with the matching ID. Then, we can toggle its “completed” boolean value. Your functions should look like: 

```react
function toggleComplete(id) {
    setTodos(
      todos.map(todo => {
        if (todo.id === id) {
          return {
            ...todo,
            completed: !todo.completed
          };
        }
        return todo;
      })
    );
  }
```

Take this function and pass it to the TodoList component. Modify the following line in the return statement of App.js: 

```react
<TodoList todos={todos} toggleComplete = {} />
```

In **TodoList.js**, destructure the toggleComplete function from the properties and pass it again to the Todo function. 

```react
function TodoList({ todos, toggleComplete }) {
    return(
        <ul>
            {todos.map(todo => (
                <Todo todo={todo} toggleComplete = {toggleComplete} />
            ))}
        </ul>
    );
}
```



We want the toggleComplete function to fire when we hit the checkbox. To do this, make a new function in **Todo.js** in **Todo()** called **handleCheckboxClick()**. Call toggleComplete with the todo’s ID. Add the property to the checkbox. 

```react
function Todo({ todo, toggleComplete }) {
 
    function handleCheckboxClick() {
        toggleComplete(todo.id);
    }
 
    return (
        <div style = {{display: "flex"}}>
            <input type = "checkbox" onClick = {handleCheckboxClick} />
```



Let’s work on functionality for removing a todo item. Switch back to **App.js** and create a new function called **removeTodo()**. Call setTodos with a new todos array passed to it with a removed todos. A helpful function for removing items from arrays is **filter()**, which, when passed the ID of the todo we want to delete, can iterate through the array and look for the undesired item. 

```react
function removeTodo(id) {
    setTodos(todos.filter(todo => todo.id !== id));
  }
```

Again, pass this function as a prop to TodoList. Modify this line (I restructured it into multiple lines) in the return statement. 

```react
<TodoList
  todos={todos}
  removeTodo={removeTodo}
  toggleComplete={toggleComplete}
/>
```

Destructure the function in **TodoList.js** as like before. When complete, the entirety of **TodoList.js** should look like: 

```react
import React from "react";
 import Todo from "./Todo";
 
 function TodoList({ todos, removeTodo, toggleComplete }) {
  return (
    <ul>
      {todos.map(todo => (
        <Todo
          todo={todo}
          removeTodo={removeTodo}
          toggleComplete={toggleComplete}
        />
      ))}
    </ul>
  );
 }
 
 export default TodoList;
```

In **Todo.js**, create a new function called **handleRemoveClick()** that handles removeTodo() and uses the ID. When complete, the entirety of **Todo.js** should look like: 

```react
import React from "react";
 
function Todo({ todo, toggleComplete, removeTodo }) {
 
  function handleCheckboxClick() {
    toggleComplete(todo.id);
  }
 
  function handleRemoveClick() {
    removeTodo(todo.id);
  }
 
  return (
    <div style = {{display: "flex"}}>
        <input type = "checkbox" onClick = {handleCheckboxClick} />
        <li
            style = {{
                color: "white",
                textDecoration: todo.completed ? "line-through" : null
            }}
        >
            {todo.task}</li>
        <button onClick = {handleRemoveClick}>X</button>
    </div>
 
  );
}
 
export default Todo;
```

Upon running your project (`yarn start`), you should find that your React project has the basic functionalities of a Todo List app. 

The final part of this project is to improve the aesthetics. You can use CSS or React Component Libraries like Material UI. 

### [Submit Deliverable Here](https://forms.gle/rx7nj6dEBAL9vnMQ6)
