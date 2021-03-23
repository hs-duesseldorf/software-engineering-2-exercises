# Software-Engineering 2 - Exercises

This repository, contains this very README.md with all exercises for software engineering 2 by Professor Lux @ university of applied sciences Düsseldorf.

*WIP - more exercises to come*

## Exercise 01: Maven & HTTP Basics

### What are Maven projects and why do I need them?

When you encounter a specific problem you want to solve with a Java program, you will often realize that someone else has already solved this problem before and was so kind to expose his work to the world as a free, open source library of reusable Java classes.

It would be nice to have a tool that automatically pulls those external Java libraries from the internet to your computer and make them accessible in your Java code for you.
This would also reduce the amount of errors that occur while working together on a Java project, because now the project is build exactly the same way, no matter where.

Thankfully those tools exist: [Gradle](https://gradle.org/) and [Maven](https://maven.apache.org/).
We will focus on Maven here, but all of the tasks handled by Maven can also be achieved with Gradle.

Maven projects only need a single [XML](https://en.wikipedia.org/wiki/XML) file to be described: [the project object model file, pom.xml](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html), which includes the external libraries in a `<dependencies>...</dependencies>` section, which consists of a list of `<dependency>...</dependency>` entries.
There are [much more things](https://maven.apache.org/what-is-maven.html) you can do with Maven projects but we will focus on the dependency management here!

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

### Doing

1. Create a Maven project and include the following dependencies in your ```pom.xml```: 
   ```xml
    <dependency>
        <groupId>org.apache.httpcomponents</groupId>
        <artifactId>httpclient</artifactId>
        <version>4.5.12</version>
    </dependency>
    ```

    **Help**: [How to create Java/Maven Projects in vscode](https://code.visualstudio.com/docs/java/java-project) | [How to create Maven projects in Eclipse](https://www.vogella.com/tutorials/EclipseMaven/article.html#exercise-create-a-new-maven-enabled-project-via-eclipse)

2. Use ```BufferedReader``` and ```InputStreamReader``` which are already included in your java development kit (JDK) so you do not need to include them as dependencies in your `pom.xml` and ```CloseableHttpClient```, ```HttpGet``` and ```HttpResponse``` from the maven dependency `org.apache.httpcomponents` you've just included in your `pom.xml` to call any website ([simple, primitive Web 1.0 website examples](https://gizmodo.com/23-ancient-web-sites-that-are-still-alive-5960831)) and return the HTTP response in the terminal.

    **Information 1**: We do not use the standard HTTP Client class from your JDK here, because otherwise we would need to handle closing the connections ourselves.

    **Information 2**: you can use other classes in your java files with the `import` key word, outside of your own class definition.

## Exercise 02: Sending JSON with HTTP POST

Another very popular use of HTTP in addition to reading websites is to build RESTful web-services that can be consumed by client applications, like for example a mobile app.
RESTful includes the word REST, which stands for **re**presentational **s**tate **t**ransfer, and the suffix `ful`, which spoilers the fact that RESTful web-services can be less or more RESTful depending on how much they follow the REST standard and its [constraints](https://en.wikipedia.org/wiki/Representational_state_transfer).

RESTful [APIs](https://en.wikipedia.org/wiki/API) (application programming interfaces) focus on resources, which data can be transferred via HTTP. So one core idea is that when you want to receive (HTTP GET) data from a server you request the address of the resource just the way you would request the HTML resource of a website and the server or the service sends you back (response message) what you requested. Or when you want to send data (HTTP POST) to a server/service you bundle the data into http message body and send it to the address of a resource.

[There is much to learn about RESTful web-services](https://spring.io/guides/gs/rest-service/) and APIs which is not part of this exercise but one main advantage over similar technologies is that it mainly uses the HTTP protocol and its messages so you do not need to learn yet another protocol.
### Doing

1. Read through [all HTTP methods](https://developer.mozilla.org/de/docs/Web/HTTP/Methods) and write down what they request, if their request has a body and if their response has a body
2. Create a maven project with the following two dependencies:
    ```xml
    <dependencies>
      <dependency>
        <groupId>org.apache.httpcomponents</groupId>
        <artifactId>httpclient</artifactId>
        <version>4.5.13</version>
      </dependency>
      <dependency>
        <groupId>org.json</groupId>
        <artifactId>json</artifactId>
        <version>20201115</version>
      </dependency>
    </dependencies>
    ```
3. Use `JSONObject` from `org.json`, `HttpPost`, `HttpResponse`,` HttpHeaders`, `CloseableHttpClient`, `StringEntity` from `org.apache.httpcomponents` and `BufferedReader` and `InputStreamReader` from your JDK to send a HTTP Post request to `https://jsonplaceholder.typicode.com/posts` which includes a JSON string including the `title` and `body` property from this resource and print out the response in the terminal.

    **Information 1**: [A JSON file](https://en.wikipedia.org/wiki/JSON) lists a bunch of `"key": "value"` pairs...
      ```json
      {
        "userId": 1,
        "id": 1,
        "title": "a very nice title",
        "body": "a very nice post body",
        "children": []
      }
      ```
    The main advantage over XML is that the resulting information is a bit more readable for humans and also the number of characters is reduced.

    **Information 2**: The [JSONObject class](https://github.com/stleary/JSON-java) can bundle JSON files into a java objects.

## Exercise 03: Docker Java container basics hands-on

Operating system like windows and linux provide an abstraction of the underlying hardware and manage the resources of your computer for you. Each app/program that you start/run is loaded into the computer memory (RAM) (running app = process). This way you can run multiple apps at once and all processes exist in the memory of your computer and managed by your operating system (until they are ended/killed).

Sometimes it is needed to somehow disconnect those processes from the underlying operating system a bit more. Also while developing software you often encounter the annoying situation where you need to setup the very same software libraries, additional needed services or other software to make your software working. Mostly you want to speed up those "setup" routines. Both, the stronger process encapsulation and the faster setup, is doable with containering. Container virtualisation technologies bundle each process within a container and then run each container as a process ontop of a host operating system and let each container connect to the underlying host operating system kernel. Depending on the container format / standart / technology there can be a container management daemon between the containrized apps and the host operating system like with [Docker](https://www.docker.com/). Another and further developed technologies are for example [Podman](https://podman.io/) or [LXD](https://linuxcontainers.org/lxd/introduction/) but most container technologies are availible only for Linux and Docker can nowadays be installed on Windows, too.
The container technology is also one if not *the* the core technology for various cloud services and products, i.e. google cloud, microsoft azure, amazon web services and so on.

### Doing

- Install docker on your computer
  - Ubuntu:
    ```
    sudo apt install docker.io
    sudo groupadd docker
    sudo usermod -aG docker $USER
    reboot
    ```
  - Windows and MacOS: https://docs.docker.com/get-docker/
- Create MyApp.java
  ```java
  public class MyApp {
    public static void main(String[] args) {
        System.out.println("This is my app");
    }
  }
  ```
- create a file called `Dockerfile` and put the following lines inside
  ```dockerfile
  FROM openjdk:11
  COPY . /usr/src/myapp
  WORKDIR /usr/src/myapp
  RUN javac MyApp.java
  CMD ["java", "MyApp"]
  ```
- navigate to the directory where you've just created `MyApp.java` and `Dockerfile` and run the following command to build a docker container from the instructions inside the `Dockerfile` and with the java code inside `MyApp.java`:
  ```bash
  docker build -t my-java-container-image-name .
  ```
- now that your container image has been built you can run a new container instance built from this container image with
  ```bash
  docker run --name my-java-app my-java-container-image-name
  ```

## Further Exercises

Further exercises are available in German here: [OneDrive Prof. Dr. Lux HSD](https://my.hs-duesseldorf.de/site/lux_w/_layouts/15/onedrive.aspx?csf=1&e=yIdSsr&FolderCTID=0x012000E51D335DB010414BA1B90B9EA9488B61&id=%2Fsite%2Flux%5Fw%2FDocuments%2FSP2010%2FSoftware%20Engineering%2FSoftware%20Engineering%20II%2F%C3%9Cbung)