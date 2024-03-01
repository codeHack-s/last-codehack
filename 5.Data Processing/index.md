# Data Processing Guide with React, Express, and MySQL

This guide provides a comprehensive overview of data processing in web applications using React, Express, and MySQL. It covers a wide range of topics including form handling, file uploads, working with JSON data, and data validation.

## Table of Contents

1. Form Handling
2. File Uploads
3. Working with JSON Data
4. Data Validation

## Introduction and Prerequisites

### How to set up a React project

We can create a new React project using vite

```bash
    npm init vite@latest
```
We will set up tailwind for faster styling and add daisy UI

### The default vite template explained

The default vite template comes with a few files and folders:


### How to set up an Express project

We can create a new Express project using npm

```bash
    mkdir backend
```

```bash
    npm init -y
```
This will create a new package.json file in the backend directory.
The package.json file is used to manage the dependencies and scripts for the project.

### What are dependencies and devDependencies?

Dependencies are packages that the project needs to run, while devDependencies are packages that are only needed for development.

**Example**
- Express is a dependency because the project needs it to run.
- Nodemon is a devDependency because it's only needed for development.

```bash
    npm install express
```

```bash
    touch index.js
```

```javascript
    const express = require("express");
    const app = express();
    app.listen(3000);
```

## Form Handling
What are forms?
Forms are a way to collect data from the user. In HTML, forms are used to collect user input. The data is then sent to the server for processing.
Data can be collected from the user in a variety of ways, including text fields, radio buttons, checkboxes, and more.

Data can be sent to the server using the GET or POST method. The GET method sends the data as part of the URL, while the POST method sends the data in the body of the request.**We studied this in the previous guide**

### Why we need data processing in forms
When a user submits a form, the data needs to be processed on the server. This can include validating the data, saving it to a database, or sending it to another service.

### Why we need data
Data is the foundation of web applications. It can be used to personalize the user experience, make decisions, and provide valuable insights.
**Example**
- A user submits a form with their name and email address. This data can be used to send them a welcome email or add them to a mailing list.
- A user submits a form with their credit card information. This data needs to be securely processed and stored to complete a purchase.

### JSX
JSX is a syntax extension for JavaScript. It is used with React to describe what the UI should look like. JSX produces React "elements" which are used to build the UI.

```jsx
const element = <h1>Hello, world!</h1>;
```

### Controlled Components
In React, forms are handled using controlled components. A controlled component is a form element whose value is controlled by React. The value is stored in the component's state and updated using the `onChange` event.

Here's a basic example:

```jsx
import React, { useState } from "react";

function Form() {
  const [value, setValue] = useState("");

  const handleChange = (event) => {
    setValue(event.target.value);
  };

  const handleSubmit = (event) => {
    alert("A name was submitted: " + value);
    event.preventDefault();
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" value={value} onChange={handleChange} />
      </label>
      <input type="submit" value="Submit" />
    </form>
  );
}

export default Form;
```

## Common React Hooks

### useState
The `useState` hook is used to add state to functional components. It returns an array with two elements: the current state value and a function that updates the state.

```jsx
const [value, setValue] = useState("");
```

### useEffect
The `useEffect` hook is used to perform side effects in functional components. It takes a function as an argument, which will be called after the component is rendered.

```jsx
useEffect(() => {
  console.log("Component rendered");
}, []);
```

### Other Available Hooks
- `useContext` - for accessing context in functional components
- `useReducer` - for managing state in a more complex way
- `useCallback` - for memoizing functions
- `useMemo` - for memoizing values
- `useRef` - for accessing DOM elements or storing mutable values

**This will be discussed in The Future Guide(Paid)**
[FutureSpace](futureSpace.co.ke)

## File Uploads

In Express, you can use middleware like `multer` to handle file uploads. Here's a basic example:

```javascript
const express = require("express");
const multer = require("multer");
const upload = multer({ dest: "uploads/" });

const app = express();

app.post("/upload", upload.single("file"), (req, res) => {
  res.send("File uploaded!");
});

app.listen(3000);
```

### How to store file uploads in a database

Files cannot be stored directly in a database. Instead, you can store the file path or URL in the database and save the file to the server.

Here's a basic example:

```javascript
app.post("/upload", upload.single("file"), (req, res) => {
  const file = req.file;
  const filePath = file.path;

  //TODO! Save the file path to the database
  res.send("File uploaded!");
});
```

## MySQL

MySQL is an open-source relational database management system. It is used to store and manage data in web applications.
Relational databases store data in tables, which are made up of rows and columns. Each row represents a record and each column represents a field.

### How to connect to a MySQL database

In Express, you can use the `mysql` package to connect to a MySQL database. 
We can also use the `mysql2` package which is a modern MySQL client for Node.js.

```bash
    npm install mysql2
```

```javascript
const mysql = require("mysql2");

const connection = mysql.createConnection({
  host: "localhost",
    user: "root
    password: "password",
    database: "mydatabase",
});

connection.connect((err) => {
  if (err) throw err;
  console.log("Connected to MySQL");
});
```

Here's a basic example of how to connect to a MySQL database in Express:

```javascript
const mysql = require("mysql");

const connection = mysql.createConnection({
  host: "localhost",
    user: "root",
    password: "password",
    database: "mydatabase",
});

connection.connect((err) => {
  if (err) throw err;
  console.log("Connected to MySQL");
});
```

### How to perform CRUD operations

CRUD stands for Create, Read, Update, and Delete. These are the basic operations for managing data in a database.

Here's a basic example of how to perform CRUD operations in Express:

```javascript
app.post("/user", (req, res) => {
  const { name, email } = req.body;
  const user = { name, email };

  connection.query("INSERT INTO users SET ?", user, (err, result) => {
    if (err) throw err;
    res.send("User added to the database");
  });
});

app.get("/users", (req, res) => {
  connection.query("SELECT * FROM users", (err, results) => {
    if (err) throw err;
    res.json(results);
  });
});

app.put("/user/:id", (req, res) => {
  const { name, email } = req.body;
  const user = { name, email };
  const id = req.params.id;

  connection.query("UPDATE users SET ? WHERE id = ?", [user, id], (err, result) => {
    if (err) throw err;
    res.send("User updated in the database");
  });
});

app.delete("/user/:id", (req, res) => {
  const id = req.params.id;

  connection.query("DELETE FROM users WHERE id = ?", id, (err, result) => {
    if (err) throw err;
    res.send("User deleted from the database");
  });
});
```

### How to handle database errors

In Express, you can use `try...catch` blocks to handle database errors. Here's a basic example:

```javascript
app.post("/user", (req, res) => {
  try {
    const { name, email } = req.body;
    const user = { name, email };

    connection.query("INSERT INTO users SET ?", user, (err, result) => {
      if (err) throw err;
      res.send("User added to the database");
    });
  } catch (err) {
    res.status(500).send("Database error");
  }
});
```

In React, you can use the `fetch` function or libraries like `axios` to send and receive data from a MySQL database. Here's a basic example with `fetch`:

```jsx
fetch("/users")
  .then((response) => response.json())
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```


## Working with JSON Data

### What is JSON?

JSON (JavaScript Object Notation) is a lightweight data interchange format. It is easy for humans to read and write and easy for machines to parse and generate.
**Example**
```json
{
  "name": "John Doe",
  "age": 30,
  "email": "john@code.hacks"
}
```
**Note** As you can see from the example above, JSON data is written as key-value pairs. Each key is followed by a colon and the key-value pairs are separated by commas.
JSON lacks data types, so all values are treated as strings. This means that you need to parse the data to use it in JavaScript.

In Express, you can use `express.json()` middleware to parse incoming JSON data. Here's how you can handle a POST request with JSON data:

```javascript
app.post("/data", (req, res) => {
  console.log(req.body);
  res.send("Data received!");
});
```

In React, you can use the `fetch` function or libraries like `axios` to send and receive JSON data. Here's a basic example with `fetch`:

```jsx
fetch("/data", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(data),
})
  .then((response) => response.json())
  .then((data) => {
    console.log("Success:", data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

## Data Validation

In Express, you can use libraries like `express-validator` to validate and sanitize data. This is called "server-side validation".
Here's a basic example:

```javascript
const { body, validationResult } = require("express-validator");

app.post(
  "/user",
  [
    body("username").isLength({ min: 5 }),
    body("email").isEmail(),
    body("password").isLength({ min: 5 }),
  ],
  (req, res) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
      return res.status(400).json({ errors: errors.array() });
    }

    //TODO! Save the user to the database
  }
);
```

In React, you can validate form inputs using state. This is called "client-side validation".
 Here's a basic example:

```jsx
const [username, setUsername] = useState("");
const [usernameError, setUsernameError] = useState("");

const validateUsername = () => {
  if (username.length < 5) {
    setUsernameError("Username must be at least 5 characters long");
  } else {
    setUsernameError("");
  }
};

// Call validateUsername whenever the username changes
useEffect(() => {
  validateUsername();
}, [username]);
```

## Contributing

We welcome contributions from the community. If you have any suggestions or improvements, feel free to open an issue or submit a pull request.
