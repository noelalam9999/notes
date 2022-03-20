# Backend
## Back-end vs front-end
- Back-end code is executed on the server, whereas front-end code is executed on the client (e.g. the browser, or a mobile app).
- The server environment can be 100% controlled, whereas on the client you only have control over the code you write.

## Web server
- A web server listens for incoming requests on a specified port.
- An HTTP web server works with the request-response model.
- mail server uses different protocol, just like FTP

## Node JS
- Node is a JavaScript implementation running on the server.
- based on V8 engine on chrome
- It provides asynchronous I/O. (input output, asynchronous - things happen all the time)
- accessing RAM is in nano seconds, disk is mili seconds, even worse with network request
- other programming languages - multi threading and parallel execution
- It doesn’t have the window object, and any other properties that are bound to the browser. Instead it offers several server-side functionalities like an HTTP web server, utilities to operate on files, etc.
- Code can be separated in different files (“modules”) and then exported / imported.
- It offers a package manager to manage dependencies.

## NPM
- package.json file - tracking dependencies, running tests
- node modules - saved locally with the project, not installed globally
- npm uninstall - removes 
- if only for development `-D`
- npm website to search for modules
  - how do we know a module is good? 
    - number of downloads, when was last update, tests
    - number of issues - the lower the better
    - community adoption, documentation

## Errors
- When an exception is “thrown”, if it’s not “caught”, it causes the execution to stop and exit with an error.
- If an exception is thrown inside of a try statement it gets passed to its catch part.

## MVC
- It means “model-view-controller”.
- It’s a web server design pattern that aims at improving modularity and separation of concerns.
- Each request is passed to its corresponding controller, which is like the “traffic director” of the required operations for that request.
- The model represents your data.
- The view is a template that when filled with data generates the final render, and represents what the user will see in terms of UI.
- The controller “interacts” with the model and the view as necessary, and then sends the response.
- router sits a bit away from the MVC and basically points to the correct resources


## Express
- Is a Node JS framework that aims to simplify a web server setup.
- Provides chainable middleware in the form of app.use(), which accepts handler callbacks that get passed the request and response object of each HTTP transaction, together with a next() callback to move to the next middleware in the chain.
- Augments Node’s req and res objects.
- Offers a Router class to easily create routes.