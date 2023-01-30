# Lab Report 2: Servers and Bugs

## A Simple String Web Server

Let's create a web server that can handle paths of this form:

```
/add-message?s=<string>
```

> In the example above, `/add-message` is the path and `s=<string>` is the query.

Our web server will take the string provided in the query and add it to our running string to be printed to the webpage.

Here's some code to start. It is not important to know what exactly the code is doing but it is generally responsible for starting up and running the server.

```
// Credit to Professor Joe Politz for the code

// A simple web server using Java's built-in HttpServer

// Examples from https://dzone.com/articles/simple-http-server-in-java were useful references

import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;

import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

interface URLHandler {
    String handleRequest(URI url);
}

class ServerHttpHandler implements HttpHandler {
    URLHandler handler;
    ServerHttpHandler(URLHandler handler) {
      this.handler = handler;
    }
    public void handle(final HttpExchange exchange) throws IOException {
        // form return body after being handled by program
        try {
            String ret = handler.handleRequest(exchange.getRequestURI());
            // form the return string and write it on the browser
            exchange.sendResponseHeaders(200, ret.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(ret.getBytes());
            os.close();
        } catch(Exception e) {
            String response = e.toString();
            exchange.sendResponseHeaders(500, response.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(response.getBytes());
            os.close();
        }
    }
}

public class Server {
    public static void start(int port, URLHandler handler) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);

        //create request entrypoint
        server.createContext("/", new ServerHttpHandler(handler));

        //start the server
        server.start();
        System.out.println("Server Started! Visit http://localhost:" + port + " to visit.");
    }
}
```

Now it is time to write the handler specifically for our program's purpose. If the path matches `/add-message`, we look for the parameters in the query. If the first parameter of the query matches `s`, the second parameter will be added to the running string. If the path does not match what we expected or if the first parameter does not match what we expected, we will print the error 404 message. The code shown below does not cover all edge cases such as when the path matches but there is no query or if the first parameter of the query is `s` but there are no other parameters. In these cases, Java automatically displays an error message.

Here's the code:

```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String ERROR_404_MESSAGE = "404 Not Found!";
    String message = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/add-message")) {
            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s")) {
                message = message + parameters[1] + "\n";
                return message;
            }
            else {
                return ERROR_404_MESSAGE;
            }
        } else {
            return ERROR_404_MESSAGE;
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```

Here are some example outputs:

![Image](https://rojiko1.github.io/cse15l-lab-reports/assets/string-server-result-1.png)

In this example, the entire path is `/add-message?s=Hello World`. When handling the request, the path is checked first. Since the path given matches the path expected, we move onto the next test: the query. Since the first parameter of the query is what we expect, we add the second parameter, which in this case is `Hello World`, to the end of our currently empty String message along with a `\n` newline character. The last step is simply to return the String to be printed to the page.

Here's another example:

![Image](https://rojiko1.github.io/cse15l-lab-reports/assets/string-server-result-2.png)

In this example, the entire path is `/add-message?s=My name is Rohil!`. Once again, the path is checked first, then the query if the path matches. Since the path given matches the path expected and the first parameter of the query is what we expect, we add the second parameter, which in this case is `My name is Rohil!`, to the end of `message` along with a `\n` newline character. At this point, `message` should have the value: `Hello World\nMy name is Rohil!\n`.

## Detecting Bugs

Before talking about detecting and fixing bugs, there is a bit of vocabulary to know:
* Symptom: The output that results from a certain input
* Failure-inducing input: Input that triggers a particular symptom
* Bug: Issue with code that results in symptoms from failure-inducing input

Let's look at an example of buggy code to explore how one may go about fixing the issue:

```
  // Averages the numbers in the array (takes the mean), but leaves out the
  // lowest number when calculating. Returns 0 if there are no elements or just
  // 1 element in the array
  static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num != lowest) { sum += num; }
    }
    return sum / (arr.length - 1);
  }
  ```

  The first step to fixing buggy code is to identify if the code is incorrect at all. We must write tests for many different possible inputs so that there is a low likelihood that a bug goes unnoticed.

  Here are a couple tests I wrote:

  ```
    @Test
  public void testAverageWithoutLast1() {
    double[] input = { 9.0, 4.5, 6.0, 10.5, 13.5, 0.0, 1.5};
    double expected = 7.5;
    assertEquals(expected, ArrayExamples.averageWithoutLowest(input), 0.0);
  }

    @Test
  public void testAverageWithoutLast2() {
    double[] input = {-4.5, -4.5, 13.5};
    double expected = 4.5;
    assertEquals(expected, ArrayExamples.averageWithoutLowest(input), 0.0);
  }
  ```

  After writing tests that cover different cases, you should run the tests with JUnit and identify if any tests fail. If a test fails, identify why the failure-inducing output resulted in the symptom demonstrated by that test. Let's use this process with my tests.

  ![Image](https://rojiko1.github.io/cse15l-lab-reports/assets/array-tests-result.png)

  As you can see, my first test passed but my second test failed. Let's investigate why the test failed and where the bug may be by tracing through the code with our failure-inducing output.

First, the function checks if the size of the array is less than 2, which is not the case. Next, the function loops through all elements in the array and keeps track of the smallest element, which in our case is -4.5. Lastly, the function loops through the elements and adds them to the sum if they are not equal to the lowest number. In our case, the first element, -4.5, will not be added, then the second element, -4.5, will not be added, then 13.5 will be added. Finally, the sum is divided by size - 1 to compute the average.

The issue is that the function doesn't add all numbers that are equal to the lowest number, not just one of them. So instead of not adding -4.5, then adding -4.5, then adding 13.5, the function does not add both of the -4.5s in the array.

Below is how I got rid of the bug. I added a new variable to keep track of whether the lowest number had been removed so that I wouldn't fail to add the lowest number more than once. Once ```foundLowest``` is set to true the first time the lowest number is found and not added, all numbers after that point will be added no matter their value.

```
static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    boolean foundLowest = false;
    for(double num: arr) {
      if(num < lowest) {lowest = num; }
    }
    double sum = 0.0;
    for(double num: arr) {
      if ((num == lowest) && (!foundLowest)) {
        foundLowest = true;
      }
      else {sum += num;}
    }
    return sum / (arr.length - 1);
  }
  ```

  ## Something I Learned

  The biggest thing I learned from lab in the past two weeks was how to create a simple Java web server that can handle requests and return some output based on the path and query. I did not know about the query part of a url beforehand despite seeing it countless times when searching on Google and I learned how one could use the query to get an input from a user, which a path, which are limited by what the developer has designed, cannot do.