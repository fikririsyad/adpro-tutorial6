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