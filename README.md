# Sprint Challenge Instructions

**Read these instructions carefully. Understand exactly what is expected _before_ starting this Sprint Challenge.**

This challenge allows you to practice the concepts and techniques learned over the past sprint and apply them in a concrete project. This sprint explored **how to build web services based on the REST (REpresentational State Transfer) architectural style**. During this sprint, you studied **Node.js and Express, server side routing, how to write Express middleware and how to deploy an API to Heroku**. In your challenge this week, you will demonstrate your mastery of these skills by **designing and creating a web API to manage the following resources: `Projects` and `Actions`**.

This is an individual assessment. All work must be your own. Your challenge score is a measure of your ability to work independently using the material covered through this sprint. You need to demonstrate proficiency in the concepts and objectives introduced and practiced in preceding days.

You are not allowed to collaborate during the sprint challenge. However, you are encouraged to follow the twenty-minute rule and seek support from your TL if you need direction.

_You have **three hours** to complete this challenge. Plan your time accordingly._

## Introduction

In meeting the minimum viable product (MVP) specifications listed below, your project should provide an API that has Create, Read, Update and Delete (CRUD) functionality for both `projects` and `actions`.

### Database Schemas

The description of the structure and extra information about each _resource_ stored in the included database (`./data/lambda.db3`) is listed below.

#### Projects

| Field       | Data Type | Metadata                                                                    |
| ----------- | --------- | --------------------------------------------------------------------------- |
| id          | number    | no need to provide it when creating projects, the database will generate it |
| name        | string    | required.                                                                   |
| description | string    | required.                                                                   |
| completed   | boolean   | used to indicate if the project has been completed, not required            |

#### Actions

| Field       | Data Type | Metadata                                                                                         |
| ----------- | --------- | ------------------------------------------------------------------------------------------------ |
| id          | number    | no need to provide it when creating posts, the database will automatically generate it.          |
| project_id  | number    | required, must be the id of an existing project.                                                 |
| description | string    | up to 128 characters long, required.                                                             |
| notes       | string    | no size limit, required. Used to record additional notes or requirements to complete the action. |
| completed   | boolean   | used to indicate if the action has been completed, not required                                  |

### Database Persistence Helpers

The `/data/helpers` folder includes files you can use to manage the persistence of _project_ and _action_ data. These files are `projectModel.js` and `actionModel.js`. Both files publish the following api, which you can use to store, modify and retrieve each resource:

**All these helper methods return a promise. Remember to use .then().catch() or async/await.**

- `get()`: resolves to an array of all the resources contained in the database. If you pass an `id` to this method it will return the resource with that id if one is found.
- `insert()`: calling insert passing it a resource object will add it to the database and return the newly created resource.
- `update()`: accepts two arguments, the first is the `id` of the resource to update, and the second is an object with the `changes` to apply. It returns the updated resource. If a resource with the provided `id` is not found, the method returns `null`.
- `remove()`: the remove method accepts an `id` as it's first parameter and, upon successfully deleting the resource from the database, returns the number of records deleted.

The `projectModel.js` helper includes an extra method called `getProjectActions()` that takes a _project id_ as it's only argument and returns a list of all the _actions_ for the _project_.

We have provided test data for all the resources.

### Commits

Commit your code regularly and meaningfully. This helps both you (in case you ever need to return to old code for any number of reasons) and your team lead as the evaluate your solution.

## Interview Questions

Be prepared to demonstrate your understanding of this week's concepts by answering questions on the following topics. You might prepare by writing down your own answers before hand.

1. The core features of Node.js and Express and why they are useful.

Node.js is a runtime environment-a program that runs other programs, a platform used to execute JavaScript applications outside the browser.

 Now JavaScript can be used to write command line utilities, native programs that run on different operating systems, networking software, web services, web applications and more.

Traditionally, the JavaScript language was only used in web browsers, but in 2009, Node.js was unveiled, and with it, the developer tool kit expanded greatly. Node.js gave developers the chance to use JavaScript to write software that, up to that point, could only be written using C, C++, Java, Python, Ruby, C# and the like.

We are using Node to write server code, specifically web services that can communicate with clients using the JSON (JavaScript Object Notation) format for data interchange.

Some of the advantages of using Node.js for writing server side code are:

JavaScript on the server: use the same programming language and paradigm for both client and server. This minimizes context switching and makes it easy to share code between the client and the server.
Single-threaded: removes the complexity involved in handling multiple threads.
Asynchronous: can take full advantage of the processor it's running on. This matters because the node process will be running on a single CPU.
Npm repository: access the largest ecosystem of useful libraries (most of them free to use) in the form of npm modules.

Expres is a light and unopinionated framework that sits on top of Node.js and makes it easier to create web applications and services. Sending an HTML file or image is now a one-line task with the sendFile helper method in Express.

Express is just a Node.js module like any other module.

Express can:

build web applications.
serve Single Page Applications (SPAs).
build RESTful web services that work with JSON.
serve static content, like HTML files, images, audio files, PDFs, and more.
power real-time applications using technologies like Web Sockets or WebRTC.

Some of the benefits of using Express are that it is:

Simple
Unopinionated
Extensible
Light-weight
Compatible with connect middleware (Links to an external site.). (This means we can tap into an extensive collection of modules written for connect.)
All packaged into a clean, intuitive, and easy to use API.
Abstracts away common tasks (writing web applications can be verbose, hence the need for a library like this)

Main Features of Express are:

Middleware
Middleware functions can get the request and response objects, operate on them, and (when specified) trigger some action. Examples are logging or security.

Express' middleware stack is basically an array of functions.

Middleware CAN change the request or response but it doesn't have to.

Routing
Routing is a way to select which request handler function is executed. It does so based on the URL visited and the HTTP method used. Routing provides a way to break an application into smaller parts.

Routers for Application Modularity
Applications can be broken up into routers. We could have a router to serve our SPA and another router for our API. Each router can have its own middleware and routing. This combination provides improved functionality.

Convenience Helpers
Express has many helpers that provide out of the box functionality to make writing web applications and API servers easier.

A lot of those helpers are extension methods added to the request and response objects.

Examples from the Api Reference (Links to an external site.) include: response.redirect(), response.status(), response.send(), and request.ip.

Views
Views provide a way to dynamically render HTML on the server and even generate it using other languages.


2. Understand and explain the use of Middleware?

Middleware can be described as an array of functions that get executed in the order they are introduced into the server code. Middleware functions can get the request and response objects, operate on them, and (when specified) trigger some action. 

The many different types of middleware fall into 3 main groups: Built-In Middleware, 3rd-Party Middleware & Custom Middleware.
All types of middleware work in the same way. First we tell Express what middleware we want to use in the app by making a call to .use() on the server & passing .use() the piece of middleware to apply. This line comes after the server has been created by calling express().

Middleware is the biggest part of Express & used to add features to Express.  Most of the code we write, including route handlers, is middleware under the hood.

3. The basic principles of the REST architectural style.

A Web API can be made scaleable and simpler to maintain and extend by applying the REST architecture which recommends the following group of principles when designing a RESTful Web API:
    Everything is a resource.
    Each resource is accessible via a unique URI.
    Resources can have multiple representations.
    Communication happens over a stateless protocol (HTTP).
    Resource management happens via HTTP methods.
	
4. Understand and explain the use of Express Routers.

Routing is a way to select which request handler function is executed. It does so based on the URL visited and the HTTP method used. Routing provides a way to break an application into smaller parts.

Routers are used for application modularity by breaking up an application into routers. A router can be used to serve the SPA and another router for the API. Each router can have its own middleware and routing which provides improved functionality.

Express Routers are a way to split an application into sub-applications to make it more modular and easier to maintain and reason about.

An Express Router behaves like a mini Express application. It can have it’s own Routing and Middleware, but it needs to exist inside of an Express application. Routers organize Express applications because separate pieces of code can later be composed together.

5. Describe tooling used to manually test the correctness of an API.

Testing APIs is different from testing websites or web applications. To test the latter, a web browser is sufficient, but for APIs, we need to be able to make POST/PUT/PATCH/DELETE requests and even modify the request headers.

For testing, we will use a tool called Postman. Postman, and other tools allow full control when making requests. We can easily change the HTTP Method used, add JSON data to the body, add form data, add headers, examine the response, and more.


You can write test scripts for your Postman API requests in JavaScript. Tests allow you to ensure that your API is working as expected, to establish that integrations between services are functioning reliably, and to verify that new developments haven't broken any existing functionality. You can also use test code to aid the debugging process when something goes wrong with your API project.

For example, you might write a test to validate your API's error handling by sending a request with incomplete data.

You can add tests to individual requests, folders, and collections. Postman includes code snippets you can click to add, then amend to suit your logic if necessary.

You are expected to be able to answer questions in these areas. Your responses contribute to your Sprint Challenge grade.

## Instructions

### Task 1: Project Set Up

- [ ] Create a forked copy of this project
- [ ] Add your team lead as collaborator on Github
- [ ] Clone your OWN version of the repository (Not Lambda's by mistake!)
- [ ] Create a new branch: git checkout -b `<firstName-lastName>`.
- [ ] Implement the project on your newly created `<firstName-lastName>` branch, committing changes regularly
- [ ] Push commits: git push origin `<firstName-lastName>`

### Task 2: Project Requirements

Your finished project must include all of the following requirements:

#### NPM Scripts

- [ ] An _npm script_ named _"server"_ that uses `nodemon`to run the API server.
- [ ] Use _nodemon_ as a development time dependency only that is not deployed to production.
- [ ] An _npm script_ named _"start"_ that uses `node` to run the API server.

#### Build an API

- [ ] Design and build endpoints for performing CRUD operations on _projects_ and _actions_. When adding an action, make sure the `project_id` provided belongs to an existing `project`. If you try to add an action with an `id` of 3 and there is no project with that `id` the database will return an error.
- [ ] Add an endpoint for retrieving the list of actions for a project.
- [ ] Use an HTTP client like `postman` or `insomnia` to test the API's endpoints.
- [ ] Use Express Routers to organize the API's code.

In your solution, it is essential that you follow best practices and produce clean and professional results. You will be scored on your adherence to proper code style and good organization. Schedule time to review, refine, and assess your work and perform basic professional polishing including spell-checking and grammar-checking on your work. It is better to submit a challenge that meets MVP than one that attempts too much and does not.

### Task 3: Stretch Goals

After finishing your required elements, you can push your work further. These goals may or may not be things you have learned in this module but they build on the material you just studied. Time allowing, stretch your limits and see if you can deliver on the following optional goals:

- [ ] Deploy the API to Heroku.
- [ ] Configure the API to support environment variables.
- [ ] Use middleware for validation of incoming data.

## Submission format

Follow these steps for completing your project.

- [ ] Submit a Pull-Request to merge <firstName-lastName> Branch into master (student's Repo). **Please don't merge your own pull request**
- [ ] Add your team lead as a reviewer on the pull-request
- [ ] Your team lead will count the project as complete after receiving your pull-request
