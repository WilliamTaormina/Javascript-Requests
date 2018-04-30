# Javascript-Requests

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

### XHR GET Requests I

When AJAX was first formalized by the World Wid Web Consortium in 2006, it required the use of an _*XMLHttpRequest*_ object, a JavaScript object that is used to retrieve data. There are several steps to creating an AJAX request or XHR, object.

![image](https://s3.amazonaws.com/codecademy-content/courses/intermediate-javascript-requests/diagrams/Asset+1.svg)

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

### XHR GET Requests II

### XHR GET Requests III

### XHR POST Requests I

### XHR POST Requests II

### XHR Post Requests III

### $.ajax() GET Requests I

### $.ajax() GET Requests II

### $.ajax() GET Requests III

### $.ajax() POST Requests I

### $.ajax() POST Requests II

### $.ajax() POST Requests III

### AJAX requests with $.get()

### AJAX requests with $.post()

### AJAX Requests with $.getJSON()

### Review Requests I
