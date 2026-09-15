#javascript #programming #web #web-security

# JavaScript

JavaScript is a high-level programming language widely used to add dynamic behaviour to web applications. In a browser, JavaScript can interact with the Document Object Model (DOM), respond to user actions, communicate with servers, manipulate application state, and process data received from web APIs.

Although JavaScript originated as a browser scripting language, modern runtimes such as Node.js also allow it to execute outside the browser. This makes JavaScript relevant to both client-side and server-side application development.

## Core Concepts

JavaScript is dynamically typed, meaning variables do not require an explicit type declaration and their values can change type during execution. Common primitive values include strings, numbers, booleans, `null`, `undefined`, `bigint`, and symbols.

Objects provide a way to represent structured data using properties and methods. Arrays are specialized objects commonly used to store ordered collections of values.

Functions are first-class values in JavaScript. They can be assigned to variables, passed as arguments, returned from other functions, and used as callbacks. This enables programming patterns based heavily on functions and asynchronous execution.

## Browser Environment

Web browsers expose JavaScript APIs that allow scripts to interact with the page and the browser environment. The DOM represents the structure of an HTML document as an object tree that JavaScript can inspect and modify.

JavaScript can also handle browser events such as clicks, keyboard input, form submission, and page loading. This event-driven model is fundamental to modern interactive web applications.

The browser executes JavaScript within a security boundary known as the same-origin policy. This restricts how scripts from one origin interact with resources belonging to another origin, although mechanisms such as CORS can allow controlled cross-origin access.

## HTTP and APIs

JavaScript applications commonly communicate with backend systems through HTTP requests. APIs frequently return structured data using JSON, which JavaScript can parse and manipulate.

This creates an important relationship between JavaScript and [[Cyber-Notes-Jr-Fundamentals/03-Web/HTTP]]. A web application may use JavaScript to collect input, construct a request, send it to an API, process the response, and update the interface without requiring a complete page reload.

## Asynchronous Execution

Web applications frequently perform operations that do not complete immediately, such as network requests, timers, or file operations. JavaScript uses an event loop and asynchronous programming mechanisms to handle these operations without blocking normal execution.

Promises and `async`/`await` provide common abstractions for working with asynchronous operations. Understanding asynchronous behaviour is important when analysing application logic, race conditions, and client-side security controls.

## Security Relevance

JavaScript is directly involved in many web vulnerabilities because it frequently processes attacker-controlled input and manipulates the DOM. Improper handling of untrusted data can lead to vulnerabilities such as Cross-Site Scripting (XSS), DOM-based injection, insecure client-side logic, and sensitive information exposure.

Client-side validation should not be treated as a security boundary because users can modify or bypass JavaScript execution. Security-sensitive validation and authorization must ultimately be enforced by the server.

JavaScript analysis is therefore an important skill when studying [[OWASP-Top-10]], [[Cyber-Notes-Jr-Fundamentals/03-Web/HTTP]], [[Cookies]], [[Sessions]], and [[Web-Architecture]].

## Related Concepts

- [[Data-Encoding]]
- [[Cyber-Notes-Jr-Fundamentals/03-Web/HTTP]]
- [[Cookies]]
- [[Sessions]]
- [[Web-Architecture]]
- [[OWASP-Top-10]]