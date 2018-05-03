# Old Javascript-Requests, and new Javascript Requests (ES6)

Javascript Requests - What are they, and how do they work?

## Introduction to Requests

There are numerous reasons why Javascript is the preferred language of the web. Amongst the most important reasons are JavaScript's non-blocking properties, or that it is an asynchronous language.

If a webpage has a large image as a background, should we have to wait around for the image to load before we can interact with any other part of the site? Of course not.

Most websites have to make multiple requests to work fully. The way javascript handles multiple requests, is called the _event loop_. Messages that will be sent to other websites containing code are added to a queue as certain events occur. Each message is run completely before moving onto the next one, which might cause the user to wait a long time between actions.

To prevent this, long messages are broken into smaller messages that are added to the queue when they are ready to be run. In the case of requesting information from another site, we separate the request from the response. (Request = asking another site for information) (Response = the information the website returns to us.)

The way we handle the separation between the request and the response is using a system of technologies called _Asynchronous JavaScript and XML_, or AJAX.

### HTTP Requests

Asynchronous Javascript and XML, or _AJAX_, involves requesting data over the web, which is done using HTTP requests. There are 4 commonly used types of HTTP requests:

1.  GET - receive information from other sites by sending a _query_.

2.  POST - can change information on another site, and will receive information or data is response.

3.  PUT

4.  DELETE

There are several differences between the way _GET_ and _POST_ requests are made.

A _GET_ request is like a Google search. If you navigate to Google and search for something, you might notice that all of your search terms ar added to the URL, like this:

```javascript
https://www.google.com/#q=pizza+near+union+square
```

the url is saying "Google, please retrieve a list of pizza places near Union Square". It is not adding, sending, or introducing any new information to Google.

_Post_ requests on the other hand, introduce new information to another website. Instead of sending this information in the URL of the Request, it is sent as a part of the body of the request.

### XHR GET Requests

When AJAX was first formalized by the World Wid Web Consortium in 2006, it required the use of an _*XMLHttpRequest*_ object, a JavaScript object that is used to retrieve data. There are several steps to creating an AJAX request or XHR, object.

On the first line, we create an XMLHttpRequest object, by typing '_new_', then the type of the object, which is _XMLHttpRequest()_. This is called the '_new operator_'.

The object is saved in a const called _xhr_. Throughout this request, we'll be accessing properties of this object.

On the next line, we save the URL to which we're going to make our request in a const called _url_.

Next, we set the _responseType_ of the xhr object to '_json_'.

_onreadystatechange_ is an event handler that is called whenever the value of the _readyState_ property changes. We set it equal to an anonymous function. This function will handle the response to the request.

```JavaScript
// XMLHttpRequest GET

const xhr = new XMLHttpRequest();
const url = 'http://api-to-call.com/endpoint';

xhr.responseType = 'json';
xhr.onreadystatechange = function(){
 if (xhr.readyState === XMLHttpRequest.DONE){
  // execute the code here with the response...
 }
};

xhr.open('GET',url);
xhr.send();
```

First, we check if the _readyState_ of our xhr object is equal to 'XMLHttpRequest.DONE'. If that evaluates to _true_, the code block executes. It is useful while writing a new program to log the response to the console so that you can see its structure. Later, you might change this function to add parts of the response to your webpage or do something else with it entirely.

Then, the _.open()_ method is called on the _xhr_ object, and it is passed two arguments.
Argument # 1: "GET" - the type of request
Argument # 2: url - the URL we are querying.

._open()_ creates and structures the request. It tells the request what method to use, and what URL to query.

Finally, we call the ._send()_ method on our xhr object and pass it no arguments. This is because data sent in _GET_ requests is sent as part of the URL. Calling the ._send()_ method sends the xhr object with its relevant information to the API URL.

### XHR POST Requests

Recall that in a _GET_ request, the query information is sent as part of the _URL_. However, in a _POST_ request, the information is sent to the server as part of the _body_ of the request.

This information is created and saved in the _data_ constant and sent to the API as an argument passed to the ._send()_ method.;

```javascript
// XMLHttpRequest POST
const xhr = new XMLHttpRequest();
const url = "http://api-to-call.com/endpoint";

const data = JSON.stringify({ id: "200" });

xhr.responseType = "json";
xhr.onreadystatechange = function() {
  if (xhr.readyState === XMLHttpRequest.DONE) {
    // execute the code here with the response...
  }
};

xhr.open("POST", url);
xhr.send(data);
```

Compare the code callouts above for a _GET_ request and a _POST_ request. Notice the POST request has added an additional variable called "data". Obviously, the data that we want to send to our API must be formatted properly. The particular properties and values sent will depend on the API you're using and the information you wish to send and retrieve.

The object containing this data is passed to the _JSON.stringify()_ method, which will format the object as a string. This is saved to a const called 'data'.

Everything else remains the same until the final two lines. When we call the ._open()_ method on the xhr object, we pass the argument _POST_, instead of _GET_. Finally, we pass the _data_ string to the ._send()_ method.

### $.ajax() GET Requests

In the example above, we constructed MXLHttpRequests from scratch, using vanilla Javascript to send the request and handle the response. But, repeating boilerplate GET and POST requests in this way can be tiresome.

To make this process easier, we can construct requests using some methods from the jQuery library.

Often times a project will already incude jQuery in the HTML, like so:

```html
<script src='https://code.jquery.com/jquery-3.2.1.min.js'></script>
```

The _script_ points to the jQuery CDN which allows us to use jQuery in our project.

$._ajax()_ is a method provided by the jQuery library specifically to handle AJAX requests. All parts f the request are included in a single object that is passed to the method as an argument. A full jQuery GET request is below:

```jQuery
$.ajax({
 url: 'http://api-to-call.com/endpoint',
 type: 'GET',
 dataType: 'JSON',
 success(response){
  code to execute when the request is successful...
 },
error(jqXHR, status, errorThrown){
 code to execute when response fails...
},
})
```

# New Javascript Requests (ES6)

Asynchronously requesting and responding to data is such an integral part of what developers do with Javascript that a new type of object, called a _Promise_, was added to Javascript in ES6.

A _PROMISE_ is an object that acts as a placeholder for data tht has been requested, but not yet received. Eventually, a promise will resolve to the value requested or to a reason why the request failed.

If the requested information or any error except a network error is received, the Promise is fulfilled and calls a function handle the response. If there is a network error, the promise is rejected, and will call a function to handle the error.

Consider the _fetch()_ function, which uses Promises to handle requests. Or, the ._then()_ method, to handle fulfilled and rejected Promises. And what's that I heard about async and await?

### fetch() GET Requests

```javascript
fetch('http://api-to-call.com/endpoint').then(response => {
 if (response.ok){
  return response.json();
 }
 throw new Error('Request failed!');
}, networkError => console.log(networkError.message)
).then(jsonResponse => {
 // code to execute with jsonResponse
})
});
```

On the first line, we call _fetch()_ function and pass it a single argument - the url of the API endpoint. Because this is a _GET_ request, this url will contain the url to the API and may also contain query parameters, an API key, a client ID, or information necessary to make the request.

The _fetch()_ function:

1.  creates a _request object_ using the information provided to it
2.  send that request object to the url provided
3.  returns a Promise that ultimately resolves to a response object.

_Note: because *fetch()* is a web API, not all browsers support it. To ensure that all users can run code that uses fetch, we can add a polyfill that will be used if a user doesn't have *fetch()* support in thier browser._

As you can also see in the example above, we chain a ._then()_ method to the closing parameters of the fetch function. This is where the asynchronicity of Javascript comes in - the fetch function makes the request and returns the response, and we don't call the function that will handle the response until it has been received.

The ._then()_ method takes two callback functions as parameters, the first of which handles success, and the second of which handles failure.

The first callback function takes _response_ as a parameter. _response_ is the resolution of the Promise returned by the fetch function.

## New New Javascript Requests (ES6 -> ES7)

```javascript
// async await GET

async function getData() {
  try {
    let response = await fetch("URL");
    if (response.ok) {
      let jsonResponse = await response.json();
      // code to execute with jsonResponse
    }
    throw new Error("Request Failed");
  } catch (error) {
    console.log(error);
  }
}
```
