## Backend Development Guide

This guide provides a comprehensive overview of backend development for web applications using Node.js, Express, and MySQL. It covers a wide range of topics including server-side programming, creating APIs, handling requests and responses, and connecting to databases.

### Server-Side Programming

Server-side programming, also known as backend development, involves writing scripts that run on a server. These scripts process client requests, interact with databases, and formulate responses sent back to the client.

Server-side languages are programming languages that are used to produce software that runs on the server. Examples include JavaScript (Node.js), Python, Ruby, PHP, Java, and C#. These languages handle the logic behind user interactions, data storage, and server responses.

We use server-side languages for several reasons:

1. **Data Processing**: Server-side languages handle the processing of data from the client, including form submissions, user authentication, and database interactions.
2. **Security**: Sensitive operations, such as password hashing and database queries, are handled on the server to protect data and prevent malicious client-side manipulation.
3. **Performance**: By offloading heavy processing tasks to the server, we can ensure that our web applications run smoothly on various devices regardless of their individual processing power.

In this guide, we'll use Node.js, a JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js allows us to use JavaScript, traditionally a client-side language, on the server.

You can download Node.js from the official website.
[Click Here 👇](https://nodejs.org/en/)

### Your First Node.js Application
Creating a new project

```bash
    mkdir learn
    cd learn
```
Now, we have to initialize the project using npm

```bash
    npm init or npm init -y
```
Npm will ask you some questions. You can skip them by using `-y` flag.
Installing dependencies

```bash
    npm install {package-name}
```
Example

```bash
    npm install express
```
Using the installed package

```bash
    touch {filename}.js

    if you are using windows
    Create a new file and name it {filename}.js
```
Inside the file add the following code

```javascript
    const express = require("express");
    const app = express();
    const port = 3000;

    app.get("/", (req, res) => {
        res.send("Hello World!");
    });

    app.listen(port, () => {
        console.log(`Server running at http://localhost:${port}`);
    });
```

Now, run the following command

```bash
    node {filename}.js
```
You will see the following output

    Server running at http://localhost:3000

Now, open your browser and go to the following link
    
        http://localhost:3000

You will see the following output
    
        Hello World!

*You can use the above file or create a new file as you wish as the steps below wont cover creating a new file again and again.*

### How Node.js Works

Node.js uses an event-driven, non-blocking I/O model. This means it can handle many connections concurrently. Instead of spawning new threads for each new connection (and thus increasing memory usage), Node.js operates on a single thread, using non-blocking I/O calls to support thousands of concurrent connections held in the event loop.

Here's an example of a simple Node.js server:

```javascript
const http = require("http");

const server = http.createServer((req, res) => {
  res.end("Hello World\n");
});

server.listen(8000);
```

In this code, `http.createServer()` is a method that returns a new instance of `http.Server`.

This server is set to listen for network requests on port 8000. When a request is received, the provided function is invoked with request (`req`) and response (`res`) objects, and it sends 'Hello World\n' as the response.

In computer networking, a port is a communication endpoint that allows different processes or services to connect and exchange data over a network. Ports are identified by numbers, known as port numbers, which range from 0 to 65535.

In the provided code, the server is set to listen for network requests on port 8000. This means that the server will be bound to port 8000 on the computer's network interface. When a client sends a request to the server's IP address on port 8000, the server will receive the request and respond accordingly

### Creating APIs

APIs (Application Programming Interfaces) allow different software applications to communicate with each other.

Express is a minimal and flexible Node.js web application framework that provides a robust set of features for applications.

```javascript
const express = require("express");
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(port, () => {
  console.log(`Server running at http://localhost:${port}`);
});
```

### Handling Requests and Responses

Handling HTTP requests and responses is a fundamental part of building a web API. Express provides methods to handle HTTP requests (GET, POST, PUT, DELETE) and to send responses to the client.

```javascript
app.get("/users", (req, res) => {
  res.json({ message: "GET /users" });
});

app.post("/users", (req, res) => {
  res.json({ message: "POST /users" });
});
```

### Example API to add two numbers
Using GET Method
```javascript
app.get("/add", (req, res) => {
  const { num1, num2 } = req.query;
  const sum = num1 + num2;
  res.json({ sum });
});
```
The request should be like this

    http://localhost:{PORT}/add?num1=10&num2=20

Using GET Method with params

```javascript
app.get("/add/:num1/:num2", (req, res) => {
  const { num1, num2 } = req.params;
  const sum = num1 + num2;
  res.json({ sum });
});

```
The request should be like this

    http://localhost:{PORT}/add/10/20

**Note:** This is not a good practice to send sensitive data like passwords in the URL. So, we use POST method to send data.

```javascript
//using post
app.post("/add", (req, res) => {
  const { num1, num2 } = req.body;
  const sum = num1 + num2;
  res.json({ sum });
});
```

Request should be like this

    {
        "num1":10,
        "num2":20
    }

How to use the example above

```javascript
fetch("http://localhost:{PORT}/add", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    num1: 10,
    num2: 20,
  }),
})
  .then((res) => res.json())
  .then((data) => console.log(data));
```


### Connecting to Databases

Connecting your application to a database allows you to store, retrieve, and manipulate data.

This allows for data persistence, which means that data is retained even after the application is closed or restarted.

- **Relational Databases**: Relational databases store data in tables that are related to each other through the use of primary and foreign keys. Examples include MySQL, PostgreSQL, and SQLite.
- **NoSQL Databases**: NoSQL databases store data in a non-tabular format. Examples include MongoDB, Firebase, and Redis.

### How to download MySQL

The simplest way is to install XAMPP, which includes MySQL as well as other useful tools. You can download XAMPP from the official website in the link below.
[Click Here 👇](https://www.apachefriends.org/download.html)

MySQL is a popular open-source relational database. Here's an example of how to connect to a MySQL database using the `mysql` module:

_A `module` is a collection of JavaScript functions and objects that can be used by external applications. Node.js has a set of built-in modules that we can use without installing them. We can also create our own modules and use them in our applications._

```javascript
const mysql = require("mysql");

const connection = mysql.createConnection({
  host: "localhost",
  user: "username",
  password: "password",
  database: "database",
});

connection.connect((err) => {
  if (err) throw err;
  console.log("Connected to the MySQL server.");
});
```

This code creates a connection to a MySQL server running on localhost. Replace `'username'`, `'password'`, and `'database'` with your actual MySQL username, password, and database name.

### Using the created connection

Once the connection is established, we can use the `connection` object to execute queries.

```javascript
connection.query("SELECT * FROM users", (err, rows) => {
  if (err) throw err;

  console.log("Data received from the database:");
  console.log(rows);
});
```

Example endpoint that returns all users from the database:

```javascript
app.get("/users", (req, res) => {
  connection.query("SELECT * FROM users", (err, rows) => {
    if (err) throw err;

    res.json(rows);
  });
});
```

### Contributing

We welcome contributions from the community. If you have any suggestions or improvements, feel free to open an issue or submit a pull request. Please make sure to follow the contribution guidelines.

1. Fork the repository.
2. Create a new branch for your changes.
3. Make your changes in your branch.
4. Submit a pull request from your branch to the master branch in the original repository.

We appreciate your help in making this guide better!
## The best way to learn

Practice

## Contributing

We welcome contributions from the community. If you have any suggestions or improvements, feel free to open an issue or submit a pull request.