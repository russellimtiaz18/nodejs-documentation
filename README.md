# My Node.js & Express.js Documentation

### Total Chapters are following

1. Node.js
   1. Introduction to the playlist
   2. Introduction to node.js
   3. Local Module
   4. Built-in module - fs module
   5. Built-in module - os and path module
   6. Built-in module - http module
   7. request, response, status code
   8. npm crash course
   9. http routing
   10. create node server and deploy on heroku
2. Express.js
   1. introduction to express.js
   2. express server
   3. http methods and postman
   4. Express Router
   5. HTTP Response
   6. HTTP Request part-1
   7. HTTP Request part-2
   8. HTTP Request part-3
   9. send and receive from data
   11. How to set .env variables
   12. Middlewares
   13. express static Middlewares
   14. MVC pattern

<br />

## Chapter 1: Node.js

### 1.2 Introduction to Node.js & setup

#### What is Node.js & Why Node.js?

- Node.js is server side environment; not a programming language.
- It helps to manage files (create, open, read, write, delete and close) on the server.
- it supports asynchronous programming.
- it helps to collect form data.
- It helps to manage (add, modify, delete data) database.
- fullstack = front-end + back-end

#### Environment setup

- check node is already installed or not using the command: node --version
- [Node.js](https://nodejs.org/en/) download & install
- Editor: anything; I prefer [Visual Studio Code](https://code.visualstudio.com/)

### 1.3 Local module

#### What is module? Types of module?

- Module is a set of functions or variables.
- 3 types of module.
  - local module (own created module)
  - built-in-modules (node.js own module)
  - External modules (3rd party module mainly managed by npm)
- example 1

  ```js
  // message.js
  const SUBJECT = "Node.js";

  const displayInfo = (name) => {
    console.log(`Welcome ${name}`);
  };

  module.exports = { SUBJECT, displayInfo };

  // index.js
  const message = require("./message");
  console.log(message.SUBJECT);
  message.displayInfo("Anisul Islam");
  ```

- example 2

  ```js
  // message.js

  const SUBJECT = "Node.js";
  // exports.SUBJECT = "Node.js";

  const displayInfo = (name) => {
    console.log(`Welcome ${name}`);
  };

  exports.SUBJECT = SUBJECT;
  exports.displayInfo = displayInfo;

  // index.js

  // following line will get everything from message module
  const message = require("./message");

  // following line will get separate items from message module
  const { SUBJECT, displayInfo } = require("./message");
  console.log(SUBJECT);
  displayInfo("anisul");
  ```

### 1.4 Built-in module - fs module

- some of the common built-in module - http, url, fs, path
- example of fs module

  ```js
  const fs = require("fs");
  console.log(fs);

  // creating a file
  fs.writeFile("test.txt", "this is some demo text", (err) => {
    if (err) {
      console.log(err);
    } else {
      console.log("File is created successfully");
    }
  });

  // appending data to a file
  fs.appendFile("test.txt", "some extra text is added", (err) => {
    if (err) {
      console.log(err);
    } else {
      console.log("data is added successfully");
    }
  });

  // reading data from a file
  fs.readFile("test.txt", "utf-8", (err, data) => {
    if (err) {
      console.log(err);
    } else {
      console.log(data);
    }
  });

  // renaming an existing file
  fs.rename("test.txt", "test2.txt", (err) => {
    if (err) {
      console.log(err);
    } else {
      console.log("successfully renamed");
    }
  });

  // checking a file exsits or not
  fs.exists("test2.txt", (result) => {
    if (result) {
      console.log("file exists");
    } else {
      console.log("file does not exist");
    }
  });

  // deleting a file
  fs.unlink("test2.txt", (err) => {
    if (err) {
      console.log(err);
    } else {
      console.log("file is deleted successfully");
    }
  });
  ```

### 1.5 Built-in module - os and path module

- Example of os and path module

  ```js
  // os, path
  const { totalmem, freemem } = require("os");
  console.log(os.userInfo());
  console.log(os.homedir());
  console.log(os.hostname());
  console.log(totalmem());
  console.log(freemem());

  console.log(__dirname);
  console.log(__filename);

  const path = require("path");

  const extensionName = path.extname("index.html");
  console.log(extensionName);

  const joinName = path.join(__dirname + "/../views");
  console.log(joinName);
  ```

### 1.6 Built-in module - http module

- Example of a node.js http server

  ```js
  const http = require("http");

  const PORT = 3000;

  const server = http.createServer((req, res) => {
    // res.end("welcome to the server");
    res.end("<h1>welcome to the server</h1>");
  });

  server.listen(PORT, () => {
    console.log(`server is running at http://localhost:${PORT}`);
  });
  ```

### 1.7 request, response and status code

- Example

  ```js
  // index.js file
  const http = require("http");

  const PORT = 3000;

  const server = http.createServer((req, res) => {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.write("welcome to the server");

    // if we want to return html as status
    // res.writeHead(200, { "Content-Type": "text/html" });
    // res.write("<h1>welcome to the server</h1>");

    res.end();
  });

  server.listen(PORT, () => {
    console.log(`server is running at http://localhost:${PORT}`);
  });
  ```

### 1.8 External modules | npm crash course

- first initialize npm with the command `npm init` then follow the instructions
- we can also use `npm init -y` command for ignoring the installation instructions
- npm packages : https://www.npmjs.com/
- Install https://www.npmjs.com/package/random-fruits-name package
  and follow the instructions

### 1.9 http routing

- initialize the npm `npm init -y`
- example is given below:

  ```html
  // index.html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>home</title>
    </head>
    <body>
      <nav>
        <ul>
          <li><a href="/">Home</a></li>
          <li><a href="/about">About</a></li>
          <li><a href="/contact">Contact</a></li>
        </ul>
      </nav>
      <main>
        <h1>welcome to home page</h1>
      </main>
    </body>
  </html>
  ```

  ```html
  // about.html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>about</title>
    </head>
    <body>
      <nav>
        <ul>
          <li><a href="/">Home</a></li>
          <li><a href="/about">About</a></li>
          <li><a href="/contact">Contact</a></li>
        </ul>
      </nav>
      <main>
        <h1>welcome to about page</h1>
      </main>
    </body>
  </html>
  ```

  ```html
  // contact.html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>contact</title>
    </head>
    <body>
      <nav>
        <ul>
          <li><a href="/">Home</a></li>
          <li><a href="/about">About</a></li>
          <li><a href="/contact">Contact</a></li>
        </ul>
      </nav>
      <main>
        <h1>welcome to contact page</h1>
      </main>
    </body>
  </html>
  ```

  ```html
  // error.html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>error</title>
    </head>
    <body>
      <nav>
        <ul>
          <li><a href="/">Home</a></li>
          <li><a href="/about">About</a></li>
          <li><a href="/contact">Contact</a></li>
        </ul>
      </nav>
      <main>
        <h1>page not found 404</h1>
      </main>
    </body>
  </html>
  ```

  ```js
  // index.js
  const http = require("http");
  const fs = require("fs");

  const PORT = 3000;

  const server = http.createServer((req, res) => {
    const handleReadFile = (fileName, statusCode) => {
      fs.readFile(fileName, (err, data) => {
        res.writeHead(statusCode, { "Content-Type": "text/html" });
        res.write(data);
        res.end();
      });
    };

    if (req.url === "/") {
      handleReadFile("index.html", 200);
    } else if (req.url === "/about") {
      handleReadFile("about.html", 200);
    } else if (req.url === "/contact") {
      handleReadFile("contact.html", 200);
    } else {
      handleReadFile("error.html", 404);
    }
  });

  server.listen(PORT, () => {
    console.log(`server is running at http://localhost:${PORT}`);
  });
  ```

- run the server `node index.js`

### 1.10 create node server and deploy on heroku

<br />

## Chapter 2: Express.js

### 2.1 Introduction to express.js

- Express.js is a node.js framework which makes life easier
- easy to learn and time saving facilitites available because we have ready made stuff in express.js
- MERN Stack, NERD stack, PERN stack

### 2.2 creating express server

- first initialize npm : `npm init -y`
- install express: `npm install express`
- example

  ```js
  const express = require("express");

  const PORT = 3000;

  const app = express();

  app.get("/", (req, res) => {
    res.send("<h1> Welcome to express server </h1>");
  });

  app.listen(PORT, () => {
    console.log(`server is running at http://localhost:${PORT}`);
  });
  ```

### 2.3 http methods and postman

- HTTP methods - get, post, put, patch, delete ...
- get methods helps to get a resource or data
- post method helps to create new resource
- put method helps to update a resource
- patch method helps to update single item of a resource
- delete method helps to delete a resource
- example

  ```js
  // index.js

  const express = require("express");

  const PORT = 3000;

  const app = express();

  // http://localhost:3000/user

  app.get("/user", (req, res) => {
    res.send("<h1> Welcome to get request of express server </h1>");
  });

  app.post("/user", (req, res) => {
    res.send("<h1> Welcome to post request of express server </h1>");
  });

  app.put("/user", (req, res) => {
    res.send("<h1> Welcome to put request of express server </h1>");
  });

  app.patch("/user", (req, res) => {
    res.send("<h1> Welcome to patch request of express server </h1>");
  });

  app.delete("/user", (req, res) => {
    res.send("<h1> Welcome to delete request of express server </h1>");
  });

  app.listen(PORT, () => {
    console.log(`server is running at http://localhost:${PORT}`);
  });
  ```

### 2.4 Express Router

- example

  ```js
  // step1: creates a routes folder
  // setp2: create a file name as user.routes.js
  // step3: write the following code inside user.routes.js
  const express = require("express");

  const router = express.Router();

  // /users
  router.get("/", (req, res) => {
    res.send("I am get method of user route");
  });

  router.post("/", (req, res) => {
    res.send("I am post method of user route");
  });

  router.put("/", (req, res) => {
    res.send("I am put method of user route");
  });

  router.patch("/", (req, res) => {
    res.send("I am patch method of user route");
  });

  router.delete("/", (req, res) => {
    res.send("I am delete method of user route");
  });

  module.exports = router;

  //step4: write following code inside index.js
  const express = require("express");

  const userRoutes = require("./routes/user.routes");

  const PORT = 3000;

  const app = express();

  app.use("/users", userRoutes);

  app.listen(PORT, () => {
    console.log(`server is running at http://localhost:${PORT}`);
  });
  ```

### 2.5 HTTP Response

- response can be text, html, json
- res.send("some text here");
- res.status(statuscode).json({...});
- res.sendFile(fileName);
- res.cookie(key, value);
- res.clrarCookie(key);
- res.writeHead()
- res.write()
- res.end()
- res.append(key, value); this will set as response header

### 2.6 HTTP Request part-1

- request with query parameter - req.query.parameterName
- request with route parameters - req.params.parameterName
- request with headers - req.header(key)
- request with json data / form data inside body - req.body.parameterName
- example of query parameter
  - http://localhost:3000?id=101&name=imtiaz
  - we can get the value using req.query.id and req.query.name
  ```js
  router.post("/", (req, res) => {
    console.log(req.query);
    console.log(req.query.id);
    console.log(req.query.name);
    res.send("I am get method of user route");
  });
  ```

### 2.7 HTTP Request part-2

- example of routes parameter
  - http://localhost:3000/101
  - we can get the value using req.params.id
  ```js
  router.post("/:id", (req, res) => {
    console.log(req.params.id);
    res.send("I am get method of user route");
  });
  ```
- example of how to get data header requests
  ```js
  router.post("/", (req, res) => {
    console.log(req.header("id"));
    res.send("I am get method of user route");
  });
  ```

### 2.8 HTTP Request part-3

- example of request with json data

  - first add `app.use(express.json())`; for form data use `app.use(express.urlencoded({extended: true}))`
  - then access the data using `req.body.parameterName`

  ```js
  // sending json or from data when making request
  {
    "name" : "anisul"
  }

  router.post("/", (req, res) => {
    res.status(201).json({
      message: "user is created",
      name: req.body.name,
    });
  });
  ```

### 2.9 send and receive from data

- create a index.html file inside views folder
  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <title>home</title>
    </head>
    <body>
      <nav>
        <ul>
          <li><a href="/">Home</a></li>
        </ul>
      </nav>
      <main>
        <h1>welcome to home page</h1>
        <form action="/users" method="post">
          <label for="name">Name</label>
          <input type="text" id="name" name="name" />
          <button type="submit">Register</button>
        </form>
      </main>
    </body>
  </html>
  ```
- load a html file

  ```js
  // Inside user.routes.js file
  const express = require("express");
  const path = require("path");

  const router = express.Router();

  router.get("/", (req, res) => {
    res.sendFile(path.join(__dirname, "../views/index.html"));
  });

  router.post("/", (req, res) => {
    res.status(201).json({
      message: "user is created",
      name: req.body.name,
    });
  });

  module.exports = router;

  // inside index.js
  const express = require("express");

  const userRoutes = require("./routes/user.routes");

  const PORT = 3000;

  const app = express();

  app.use(express.json());
  app.use(express.urlencoded({ extended: true }));
  app.use("/users", userRoutes);

  app.listen(PORT, () => {
    console.log(`server is running at http://localhost:${PORT}`);
  });
  ```


### 2.10 How to set .env variables

- Step 1: create an .env file in the root directory

- Step 2: define environment variable(S) using uppercase letters and underscore if more than one word. Example -
  PORT
  DATABASE_URL

- Step 3: Assign the values without double quotation and space
  PORT=3000
  DATABASE_URL=mongodb+srv://medo:demo1234@cluster0.0tl3q.mongodb.net/test?retryWrites=true&w=majority

- Step 4: you can make a comment using #

  ```
  # server port
  PORT=3000
  ```

- Step 5: install dotenv package - npm install dotenv

- Step 6: require dotenv - require('dotenv').config();

- Step 7: Access the env variables from anywhere using process.env.VARIABLE_NAME. Example ??? process.env.PORT;

- Optional: DotENV Extension - nice syntax highlighting in your .env files.

### 2.12 Middlewares

- what is middleware?
  - middleware is a function; it contains request obejct, response object and next function
- why middleware?
  - execute any code inside middleware
  - we can make changes to the request and response object
  - we can end the request and response cycle.
  - we can call the next middleware in the stack.
- Types of middleware

  - Application Level middleware: app.use(), app.METHOD(); here METHOD can be get, put, post, delete, patch
  - router Level middleware: router.use(),router.METHOD()
  - built-in Level middleware: express.json(), express.urlencoded(), express.static()
  - third-party Level middleware: body-parser
  - error handling middleware

    ```js
    // routes not found error
    app.use((req, res, next) => {
      res.status(404).json({
        message: "resource not found",
      });
    });

    // server error
    app.use((err, req, res, next) => {
      console.log(err);
      res.status(500).json({
        message: "something broke",
      });
    });
    ```

### 2.13 express static Middlewares

- `app.use(express.static());` helps us to use static resources such as css and image inside our server
