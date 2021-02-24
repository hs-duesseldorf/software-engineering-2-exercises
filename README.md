# Software-Engineering 2 - Exercises

This repository, contains this very README.md with all exercises for software engineering 2 by Professor Lux @ university of applied sciences Düsseldorf.

*WIP - more exercises to come*

## Exercise 01: Maven & HTTP Basics

### What are Maven projects and why do I need them?

When you encounter a specific problem you want to solve with a Java program, you will often realize that someone else has already solved this problem before and was so kind to expose his work to the world as a free, open source library of reusable Java classes.

It would be nice to have a tool that automatically pulls those external Java libraries from the internet to your computer and make them accessible in your Java code for you.
This would also reduce the amount of errors that occur while working together on a Java project, because now the project is build exactly the same way, no matter where.

Thankfully those tools exist: Gradle and Maven.
We will focus on Maven here, but all of the tasks handled by Maven can also be achieved with Gradle.

Maven projects only need a single [XML](https://en.wikipedia.org/wiki/XML) file to be described: [the project object model file, pom.xml](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html), which includes the external libraries in a `<dependencies>...</dependencies>` section, which consists of a list of `<dependency>...</dependency>` entries.
There are [much more things](https://maven.apache.org/what-is-maven.html) you can do with Maven projects but we will reduce our focus on the dependency management here!

### HTTP - the protocol of the internet

You probably already used a web browser to display the content of a website on your computer/smartphone.
When you've entered the address of a website and pressed the enter button your browser somehow pulled the website from the webserver and displays it in the browser window.
What internally happened could be reduced to the following steps:

- Your browser sends a HTTP _**request**_ message to the webserver which consists of
  - the request type, in this case the type is **GET**
  - the host name or the address, for example www.google.de
- The webserver sends back a HTTP _**response**_ message (according to the request type) to your computer which consists of
  - a message header, which includes 
    - a response status code in a range from [100 to 511](https://developer.mozilla.org/de/docs/Web/HTTP/Status)
    - the server-type
    - the language of the content
    - a close connection flag
    - the type of the content in the body
  - and a message body, which includes the website HTML code
- Your webbrowser renders the HTML code with its HTML render engine and displays its contents in the browser window

As you can see from the `content-type` property of the response header, HTTP messages can include different [types of content](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type), for example
- [XML](https://en.wikipedia.org/wiki/XML)
- [HTML](https://en.wikipedia.org/wiki/HTML)
- [JSON](https://en.wikipedia.org/wiki/JSON)
- regular text

Another very popular use of HTTP in addition to reading websites is to build RESTful webservices that can be consumed by client applications, like for example a mobile app.
RESTful includes the word REST, which stands for **re**presentational **s**tate **t**ransfer, and the suffix `ful`, which spoilers the fact that RESTful webservices can be less or more RESTful depending on how much they follow the REST standard.

### Doing

1. Create a Maven project and include the following dependencies in your ```pom.xml```: 
   ```xml
    <dependency>
        <groupId>org.apache.httpcomponents</groupId>
        <artifactId>httpclient</artifactId>
        <version>4.5.12</version>
    </dependency>
    ```

2. Use ```BufferedReader``` which comes already bundled with your JDK, ```InputStreamReader```,  ```CloseableHttpClient```, ```HttpGet``` and ```HttpResponse``` from the maven dependency `org.apache.httpcomponents` you've just included to call any website ([simple, primitive Web 1.0 website examples](https://gizmodo.com/23-ancient-web-sites-that-are-still-alive-5960831)) and return the HTTP response in the terminal.
3. Read through [all HTTP methods](https://developer.mozilla.org/de/docs/Web/HTTP/Methods) and write down what they request, if their request has a body and if their response has a body

## WIP Exercise 02: Docker Basics & MariaDB Image

### WIP Docker Basics

### WIP MariaDB with XAMPP

## WIP Exercise 03: Spring Boot Basics