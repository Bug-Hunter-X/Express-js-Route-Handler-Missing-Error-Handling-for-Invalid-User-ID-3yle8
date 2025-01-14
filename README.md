# Express.js Route Handler Missing Error Handling for Invalid User ID

This repository demonstrates a common error in Express.js route handlers:  missing error handling for invalid input. Specifically, the provided code attempts to parse a user ID from the request parameters as an integer without checking for potential errors, such as non-numeric input.  This can lead to crashes or unexpected behavior.

## Bug Description

The `/users/:id` route attempts to find a user based on the ID provided in the URL. However, it doesn't handle cases where the `id` parameter is not a valid integer.  If a non-numeric value is passed, `parseInt(userId)` will return `NaN`, resulting in the `users.find()` method failing to find the user, even if a user with the correct ID exists.

The bug is demonstrated in `bug.js`.  The solution, which includes robust error handling, is shown in `bugSolution.js`.

## How to Reproduce

1. Clone the repository.
2. Run `npm install` to install dependencies.
3. Run `node bug.js`.
4. Make a request to `/users/abc` (or any non-numeric ID).  You'll likely encounter a runtime error.
5. Now run `node bugSolution.js` and make the same request. The solution provides a graceful 404 response.

## Solution

The solution involves adding input validation and more robust error handling to the route handler.  The improved code in `bugSolution.js` checks if the `userId` is a number before attempting to find the user.