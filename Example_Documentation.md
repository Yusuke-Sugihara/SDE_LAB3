# SDE Lab 03: REST ADVANCED

## DOCUMENTATION: Example 01

### What is node js? Why it is called node? Why does it differ from other javascript libraries?

Node.js is a runtime environment that allows for the execution of JavaScript code server-side, using asynchronous, event-driven architecture; it is called "Node" to emphasize its intention for easily creating scalable network applications and differs from JavaScript libraries which are typically client-side and provides pre-written JavaScript code to simplify development tasks within a browser context.

In the Virtual Machine, you can see the folder named Example 1. When you open the folder using vs code, you can see there are two JSON files and one html file as shown in the figure on the side. 

### app.js: 

This file typically serves as the main entry point for defining the core logic and functionality of the application. Functions and code in this file may include:

- managing user interaction and events on the webpage, such as form submissions, button clicks and user input
- making an API request to fetch data from the server or send data to the server
- updating the user interface (UI) dynamically to reflect the changes in the application’s state
- handling routing and navigation within a single-page application (SPA).

### index.html:

It is the main HTML file of the web application and it defines the structure and content of the web page. It is the entry point of your web application and it specifies how the page is initially displayed to the user. It includes a reference to the JavaScript file that provides the application’s functionality and interactivity.
## Getting Started with the Example 01:

After you load the Example 1 folder in the VS Code, open the `app.js` file, where you see the functions and code for making API requests to fetch the humor jokes. You can see all the codes are commented on, now we will uncomment them and discuss how the code works and how API request is made. Let’s get started:

### index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Joke Fetcher App</title>
</head>
<body>
    <input type="text" id="jokePrompt" placeholder="Enter joke keyword...">
    <button onclick="fetchJoke()">Get Joke</button>
    <script src="/script.js"></script>
</body>
</html>
```

### `<button onclick="fetchJoke()">Get Joke</button>`:

A button element that the user can click to trigger a joke fetch. The `onclick` attribute is an event handler that calls the `fetchJoke()` function when the button is clicked.

### `<script src="/script.js"></script>`:

This tag links an external JavaScript file named "script.js" to the HTML document. This file is expected to contain the `fetchJoke()` function that will be executed when the user clicks the "Get Joke" button.

### app.js
```javascript
const express = require('express');
const axios = require('axios');
const path = require('path');

const app = express();
const PORT = 5600;
```
### Import necessary modules:

- `express`: a web server framework to handle HTTP requests.
- `axios`: a popular HTTP client library to make requests to the API server.
- `path`: a core Node.js module to handle file paths.

`app` is an instance of express, which you will use to define routes and handle HTTP requests.

`PORT` is set to 5600 as the port on which the server will listen for incoming requests.

```javascript
// Serve static files
app.use(express.static(path.join(__dirname, '.')));
```
This line serves static files (e.g., HTML, CSS, JavaScript) from the current directory (indicated by `__dirname`) using Express's built-in `express.static` middleware.

- `express.static`: `express.static` middleware serves static files such as HTML, CSS, and JavaScript directly from the server's current directory, providing efficient delivery of these unchanging resources.

`express.static` middleware serves static files like HTML, CSS, and images.

There are some other options for middleware:
- `express.json()` for parsing JSON bodies, which is used in Ex2.
- `express.urlencoded()`, which is for parsing URL-encoded bodies.
- Custom middleware for tasks like logging, authentication, and error handling.
```javascript
app.get('/fetchJoke', async (req, res) => {
    const apiUrl = "https://humor-jokes-and-memes.p.rapidapi.com/jokes/random";
    const prompt = req.query.prompt || '';
});
```
`app.get()` defines a route for HTTP GET requests to the endpoint '/fetchJoke'. 

- `async`: Use `async` before a function in JavaScript to handle operations that depend on promises, like I/O, querying a database, or network requests, without blocking code execution. This allows `await` to pause until the operation completes, which is essential for efficient non-blocking code execution.

- `(req, res)`: In Express, `req` handles incoming request details, and `res` is used to send back the server's response. Both are parameters in route callbacks for managing HTTP interactions.

`apiUrl` is set to the URL of an external joke API.

`prompt` is extracted from the query parameters (e.g., '/fetchJoke?prompt=somePrompt') and set to an empty string if not provided.
```javascript
app.get('/fetchJoke', async (req, res) => {
    const apiUrl = "https://humor-jokes-and-memes.p.rapidapi.com/jokes/random";
    const prompt = req.query.prompt || ''; 

    try {
        const response = await axios.get(apiUrl, {
            params: {
                'exclude-tags': 'sexist,rude,racist,yo_mamma,sexual,political,religious',
                'max-length': '200',
                'include-tags': 'one_liner',
                'min-rating': '7',
                keywords: prompt
            },
            headers: {
                'X-RapidAPI-Key': '.......',
                'X-RapidAPI-Host': 'humor-jokes-and-memes.p.rapidapi.com'
            }
        });
        res.json({ joke: response.data.joke });
    } catch (error) {
        console.error('Error fetching joke:', error);
        res.status(500).json({ error: 'Failed to fetch joke' });
    }
});
```
The `const response = await axios.get(apiUrl)` is a client-side command that waits for a response from an API request made with Axios, while `app.get('/fetchJoke', async (req, res) => { ... })` defines a server-side endpoint in an Express application that handles incoming GET requests to the '/fetchJoke' path asynchronously.

Inside this route handler, which is a function that processes requests to a specific endpoint and determines the response sent back to the client, an external API request is made using the axios library. The API request includes query parameters and headers.

The `res.json()` method in Express automatically sends a JSON response with the appropriate Content-Type header set, ensuring the client interprets the response as JSON.

If the request is successful, the response from the external API is sent as a JSON Response with the key 'joke' in the response.

If there's an error in the API request, an error message is logged, and a 500 Internal Server Error response is sent.
```javascript
try {
    const response = await axios.get(apiUrl, {
        params: {
            'exclude-tags': 'sexist,rude,racist,yo_mamma,sexual,political,religious',
            'max-length': '200',
            'include-tags': 'one_liner',
            'min-rating': '7',
            keywords: prompt
        },
        headers: {
            'X-RapidAPI-Key': 'adcfff7cd0msh65ddb9f35c37386p117c19jsn77c98eb5f0fc',
            'X-RapidAPI-Host': 'humor-jokes-and-memes.p.rapidapi.com'
        }
    });
}
```
The `await` keyword in JavaScript pauses an async function until a Promise is fulfilled, letting other code run without blocking.

This line uses Axios to make a GET request to the defined API URL. The following parameters and headers are set for the request:

- Exclude jokes with tags matching the prompt.
- Jokes should not exceed 200 characters.
- Jokes should be of the 'one_liner' tag.
- Jokes should have a minimum rating of 7.
- Jokes should have the keyword ‘prompt.

It also sets API-specific headers for authentication and identification.
```javascript
});
if (response.data.jokes && response.data.jokes.length > 0) {
    res.json({ joke: response.data.jokes[0].joke });
} else {
    res.json({ joke: "No joke found!" });
}
} catch (error) {
    console.error('Error fetching joke:', error);
    res.status(500).json({ error: `Failed to fetch joke: ${error.message}` });
}
});
```
If the code finds jokes, it sends the first one back. However, if there are no jokes, it sends back a message saying "No joke found!". If something goes wrong during the process, it logs the error and sends back a message saying there was an error trying to fetch a joke.
```javascript
app.get('/script.js', (req, res) => {
    res.type('text/javascript');
    res.send(`
        async function fetchJoke() {
            const prompt = document.getElementById('jokePrompt').value;
            try {
                const response = await fetch('/fetchJoke?prompt=' + encodeURIComponent(prompt));
                const data = await response.json();
                alert(data.joke);
            } catch (error) {
                console.error('Error:', error);
            }
        }
    `);
});
```
API Endpoint `/script.js`:

This code defines a route for HTTP GET requests to '/script.js'. The response is set to the type 'text/javascript', indicating that it's JavaScript code. The response body is a JavaScript function named `fetchJoke`. This function fetches a joke using an input prompt from the client, and upon success, it displays the joke using an alert. This code is serving a client-side script for the web page.

`const prompt = document.getElementById('jokePrompt').value;` in the JavaScript code fetches the value entered by the user into an input field with the ID `jokePrompt` on the webpage.

`encodeURIComponent(prompt)` function in JavaScript is used to safely encode a string (the user input from `prompt`) so that it can be included in a URL query string without interfering with the URL's structure by escaping special characters.

`fetch`: The fetch function in JavaScript requests data from servers and uses Promises to deal with the response later, allowing you to continue running other code while waiting for the data.
```javascript
app.listen(PORT, () => {
    console.log(`Server running on http://localhost:${PORT}`);
});
```
The express application listens on the specified ‘PORT’, and a message is logged to the console when the server starts

Now we have uncommented all the codes. 

Let's open the new terminal. After you open the terminal, first, you need to install the libraries using the command prompt: 

```bash
npm install express cors axios path
```
Doing this creates a package.json file on the side window:

```bash
npm init --yes
``````
After that, you can start the application with the following command:

```bash
node app.js
````
Doing this should now display a message. 

![Alt text](/path/to/image.png)

After this, you can go to the browser and enter `http://localhost:5600` and refresh the page.


![Alt text](/path/to/image.png)