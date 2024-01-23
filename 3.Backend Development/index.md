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

In this section, we discuss how to connect a web application to a database, including SQL databases, NoSQL databases, and ORMs.

## Contributing

We welcome contributions from the community. If you have any suggestions or improvements, feel free to open an issue or submit a pull request.