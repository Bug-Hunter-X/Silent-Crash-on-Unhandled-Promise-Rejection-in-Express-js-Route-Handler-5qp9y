# Silent Crash on Unhandled Promise Rejection in Express.js

This repository demonstrates a common but insidious bug in Express.js applications: unhandled promise rejections within asynchronous route handlers leading to silent crashes. The application appears to work until a promise in a route handler rejects, after which it stops responding without any helpful error messages.

## Problem

The `bug.js` file contains an Express.js server with a route handler that performs an asynchronous operation. This operation is designed to simulate an error by throwing an exception within its `then` block.  However, this error is not handled, resulting in a silent crash of the server. There is no error logged to the console and the server becomes unresponsive.  Standard error handling is not triggered.

## Solution

The `bugSolution.js` file demonstrates the solution:  Always handle promise rejections using `.catch()` and implement proper error handling to provide informative logging or responses to clients.  Using a process event listener for `unhandledRejection` is shown as a secondary layer of protection.

## How to run

1. Clone the repository.
2. Navigate to the repository's directory.
3. Install dependencies: `npm install`
4. Run the buggy code: `node bug.js` (Observe no crash reporting, server just stops responding)
5. Run the fixed code: `node bugSolution.js` (Observe error messages logged to the console)
