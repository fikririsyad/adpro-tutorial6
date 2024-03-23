# Tutorial 6
Fikri Risyad Indratno</br>
2206031170</br>
Advanced Programming B

---
### Commit 1 reflection notes
> What is inside the `handle_connection` function?

`handle_connection` function is used to read data from TCP stream and print it so we can see the data being sent from the browser.
1. `handle_connection` takes mutable reference to the `stream` as its argument.
1. Create a new `BufReader` instance that wraps mutable reference to the `stream`.
1. Create a variable named `http_request` to collect the lines of requests the browser sends to our server in a vector.
1. It will read the lines from `buf_reader`, unwrap it from each line, and take lines only until an empty line is encountered.
1. It will print all the lines in `http_request`.

---

### Commit 2 reflection notes
> What does the new code do in `handle_connection` function?

The updated function will send an HTTP response back to the client with `hello.html` as its content.
1. Create `status_line` variable that indicates successful response.
1. Using `fs`, the function reads the contents of `hello.html` to a string named `contents`, and stores the contents' length to `length`.
1. Create `response` variable that contains the full HTTP response.
1. Write the response to the TCP stream, and send the response back to the client.
![Commit 2 screen capture](/assets/images/commit2.png)

---

### Commit 3 reflection notes
> How to split between responses and why the refactoring is needed?

We can split it by checking the request path and handling it differently based on the path.
1. Change the `http_request` variable to `request_line` variable, and this time it will only get the first line of the HTTP request.
1. Check if the request is to / path.
1. If it is, it will assign `HTTP/1.1 200 OK` to `status_line` and `hello.html` to a new variable named `filename`.
1. If the request is to other paths, it will assign `HTTP/1.1 404 NOT FOUND` to `status_line` and `404.html` to `filename`.
1. `contents` variable now will read the content of `filename`.

The refactoring is needed to avoid duplications in the code (DRY principle) because the only differences are the value of `status_line` and which HTML file it should return. Refactoring also makes the code easier to modify if we want it to handle other paths with the same logic in the future.
![Commit 3 screen capture](/assets/images/commit3.png)