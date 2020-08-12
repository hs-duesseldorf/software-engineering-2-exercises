# Software-Engineering 2 - Exercises

This repository, contains this very README.md with all exercises for software engineering 2 by Professor Lux @ university of applied sciences Düsseldorf.

*WIP - more exercises to come*

## Exercise 01

### Idea

It would be nice to have a tool that automatically pulls the needed dependencies/external libraries before compiling the java code.
This would also reduce the amount of errors that occur while working together on a Java project.

### Doing

1. Create a Maven project and include the following dependencies in your ```pom.xml```: 
   ```xml
    <dependency>
        <groupId>org.apache.httpcomponents</groupId>
        <artifactId>httpclient</artifactId>
        <version>4.5.12</version>
    </dependency>
    ```

2. Use ```BufferedReader```, ```InputStreamReader```,  ```CloseableHttpClient```, ```HttpGet``` and ```HttpResponse``` to call any website ([simple, primitive Web 1.0 website examples](https://gizmodo.com/23-ancient-web-sites-that-are-still-alive-5960831)) and return the HTTP response in the terminal.