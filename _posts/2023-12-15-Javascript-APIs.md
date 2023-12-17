---
title: Work With Multiple Github Accounts on The Same Computer
date: 2023-12-15 08:35:01 +/-TTTT
tags: Javascript     # TAG names should always be lowercase
---

This post is an extension of codeacademy's [intermediate Javascript coursework](https://www.codecademy.com/courses/learn-intermediate-javascript), providing more examples for the most common HTTP commands with APIs, and boilerplate templates for any use case.

Below, I discuss how to use the GET, POST, PUT, and Delete commands. 

## Defining Terminology
**HTTP commands**, also known as HTTP methods or HTTP verbs, are a set of request methods used in the [Hypertext Transfer Protocol](https://en.wikipedia.org/wiki/HTTP) (HTTP) to indicate the desired action to be performed on a given resource. These methods are essential in defining the operation to be executed on the server-side and are key in the functioning of web services.

1. **GET**: Used to request data from a specified resource. GET requests should only fetch data and not cause any other effect.
2. **POST**: Used to send data to the server to create a new resource. Typically used when submitting form data or uploading a file.
3. **PUT**: Used to update an existing resource on the server. It replaces the current representation of the target resource with the request payload.
4. **DELETE**: Used to delete a specified resource from the server.

Since interacting with servers over the internet is not an instantaneous event, Javascript (version ES6 and greater) provides an object called a **Promise** to handle asynchronous events. A Promise represents the eventual completion (or failure) of an asynchronous operation and its resulting value resolves to one of these states: Pending, Fulfilled, or Rejected.

The `fetch` function in JavaScript is a modern, versatile, and powerful API used for making network requests. It provides a more flexible and efficient way to make HTTP calls to servers than older methods. The fetch method:
1. Creates a request object that contains relevant information that an API needs.
2. Sends that request object to the API endpoint provided.
3. Returns a promise that ultimately resolves to a response object, which contains the status of the promise with information the API sent back.

## GET Requests using Fetch

```javascript
// fetch GET
const getData = async () => {
    try {
        const response = await fetch('http://api-to-call.com/endpoint');        // sends request
        if (response.ok) {                                                      // handles successful response
            const jsonResponse = await response.json();
            // code to execute with jsonResponse
        }
        throw new Error('Request Failed');                                      // handles unsuccessful response
    } catch(error) {
        console.log(error);
    }
}
```

## POST Requests using Fetch
```javascript
// fetch POST
const getData = async () => {
    try {
        const response = await fetch('http://api-to-call.com/endpoint', {       // sends request
            method: 'POST',                                                     // information for POST
            body: JSON.stringify({id:200})
        });        
        if (response.ok) {                                                      // handles successful response
            const jsonResponse = await response.json();
            // code to execute with jsonResponse
        }
        throw new Error('Request Failed');                                      // handles unsuccessful response
    } catch(error) {
        console.log(error);
    }
}
```

## PUT Requests using Fetch
```javascript
// fetch PUT
const updateData = async () => {
    try {
        const response = await fetch('http://api-to-call.com/endpoint', {       // sends request
            method: 'PUT',                                                      // information for PUT
            headers: {
                'Content-Type': 'application/json'                              // format of data you are sending
            },
            body: JSON.stringify({id:200, newData: 'Your new data here'})       // include data to update
        });        
        if (response.ok) {                                                      // handles successful response
            const jsonResponse = await response.json();
            // code to execute with jsonResponse
        }
        throw new Error('Request Failed');                                      // handles unsuccessful response
    } catch(error) {
        console.log(error);
    }
}
```

## DELETE Requests using Fetch
```javascript
// fetch DELETE
const deleteData = async () => {
    try {
        const response = await fetch('http://api-to-call.com/endpoint', {       // sends request
            method: 'DELETE',                                                   // information for DELETE
            headers: {
                'Content-Type': 'application/json'                              // format of data you are sending
            },
            body: JSON.stringify({id:200})                                      // include data to identify what to delete
        });        
        if (response.ok) {                                                      // handles successful response
            console.log('Data Deleted Successfully');
            // additional code if needed
        }
        throw new Error('Request Failed');                                      // handles unsuccessful response
    } catch(error) {
        console.log(error);
    }
}
```

## Conclusion: Constructing API URLs
Depending on the API you are working with, endpoints and formatting may change however the large majority of requests are made in the following format. 

```javascript
const baseUrl = 'http://api-to-call.com';
const requestEndpoint = '/endpoint';
const requestParams = `?api_key=${your-api-key}`;                               // query parameters add more specificity to requests
const makeApiUrl = baseUrl + requestEndpoint + requestParams;
```