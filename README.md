# Testcase for bug in electron's `net` module that prevents reading the body of an HTTP request that reponds with an error

Starting with electron@7, reading the body of a response with an error status code is impossible.

On electron@6, it is possible to do so. The `statusCode` is given, so the user can check for an error.

In this repo, we test this by launching a simple HTTP server, and running a simple script that makes such requests,
using multiple versions of electron.

Simply do:
```bash
npm i
npm start
```

When running this, we can see that in electron@6 all requests succeed : even in case of errors, one can read the repsponse.

On electron@7 however, all requests that give an HTTP error code fail. Of course, in case of error, reading the body is
invaluable, as it often gives API-specific error codes & messages, in addition to the status code.
