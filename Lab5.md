# **Lab Report 5:  Debugging**
---------
# Part 1) Debugging Scenario 

Student Post on EdStem : 
---------
What environment are you using (computer, operating system, web browser, terminal/editor, and so on)?

I am using VSCode on my macbook.

Detail the symptom you're seeing. Be specific; include both what you're seeing and what you expected to see instead. Screenshots are great, copy-pasted terminal output is also great. Avoid saying “it doesn't work”.

What I am seeing: I am seeing two completely different scores (0/4 and 4/4). 

What I expected to see: The file does exist, so I was expecting  the terminal to reflect that. There should only be one score, and for this specfic github link, I was expecting to see a score of 2/4. 
Here is a screenshot of the output:

![Image](Screen%20Shot%202023-06-03%20at%202.52.23%20PM.png)

Here are screenshots of my code: 

![Image](Screen%20Shot%202023-06-03%20at%202.53.42%20PM.png)
![Image](Screen%20Shot%202023-06-03%20at%202.53.51%20PM.png)

Detail the failure-inducing input and context. That might mean any or all of the command you're running, a test case, command-line arguments, working directory, even the last few commands you ran. Do your best to provide as much context as you can.

Command I ran: bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-lab3 
Working directory: /Users/andreac/labweek9scenario2/list-examples-grader 

TA Response:
---------
Hi there! I suggest reviewing inputs in bash shells (for example, $0, $1, $2, etc), specfically what parts of command-line arguments $0 refers to. 
In addition to this, I noticed a small issue in the line you mentioned:

```java -cp $CPATH org.junit.runner.JUnitCore > junit-output.txt``` 

The general idea is correct; however, it seems you are missing a part in the command part in your attempt in redirection (recall that a simple format of redirection is ```command > filename``` ): the part in the command that specifies the test class to be executed.

I hope that with these tips you are closer to completing your goals in this assignment. Please let me know if any other issues or questions arise!

Student Response:
---------
![Image](Screen%20Shot%202023-06-03%20at%203.48.21%20PM.png)

Thank you! I realized that $0 was incorrect and did not refer to the github link. I had forgotten that while bash is not considered, grade.sh actually was (so this was what $0 referred to). Because of this, $1 would refer to the link. I also now understand the importance of having "TestListExamples" in ```java -cp $CPATH org.junit.runner.JUnitCore > junit-output.txt``` . Without it, my code did not have the test class that contains the information needed in order to measure inputs with and output a correct score. This explains why no failures were reported and why it gave an output of 4/4. 

Information about the setup:
---------
- the file and directory structure (should have at least a java file and a bash script)
![Image](Screen%20Shot%202023-06-03%20at%204.11.06%20PM.png)

- the contents of each file before fixing the bug: 

grade.sh: 
```CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'
rm -rf student-submission
git clone $0 student-submission
echo 'Finished cloning'
if [[ -f student-submission/ListExamples.java ]]
then
  echo 'ListExamples.java found'
else
  echo 'ListExamples.java not found'
  echo 'Score: 0/4'
fi
cp student-submission/ListExamples.java ./
javac -cp $CPATH *.java
java -cp $CPATH org.junit.runner.JUnitCore > junit-output.txt
FAILURES=`grep -c FAILURES!!! junit-output.txt`
if [[ $FAILURES -eq 0 ]]
then
  echo 'All tests passed'
  echo '4/4'
else
  RESULT_LINE=`grep "Tests run:" junit-output.txt`
  COUNT=${RESULT_LINE:25:1}
  echo "JUnit output was:"
  cat junit-output.txt
  echo ""
  echo "--------------"
  echo "| Score: $COUNT/4 |"
  echo "--------------"
  echo ""
fi
```

junit-output.txt: 
```
JUnit version 4.13.2

Time: 0

OK (0 tests)

```

GradeServer.java: 
```
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.URI;
import java.net.URISyntaxException;
import java.util.Arrays;
import java.util.stream.Stream;

class ExecHelpers {

  /**
    Takes an input stream, reads the full stream, and returns the result as a
    string.

    In Java 9 and later, new String(out.readAllBytes()) would be a better
    option, but using Java 8 for compatibility with ieng6.
  */
  static String streamToString(InputStream out) throws IOException {
    String result = "";
    while(true) {
      int c = out.read();
      if(c == -1) { break; }
      result += (char)c;
      System.out.println(System.currentTimeMillis() + "; just read: " + (char)c);
    }
    return result;
  }

  /**
    Takes a command, represented as an array of strings as it would by typed at
    the command line, runs it, and returns its combined stdout and stderr as a
    string.
  */
  static String exec(String[] cmd) throws IOException {
    Process p = new ProcessBuilder()
                    .command(Arrays.asList(cmd))
                    .redirectErrorStream(true)
                    .start();
    InputStream out = p.getInputStream();
    return String.format("%s\n", streamToString(out));
  }

}

class Handler implements URLHandler {
    public String handleRequest(URI url) throws IOException {
       if (url.getPath().equals("/grade")) {
           String[] parameters = url.getQuery().split("=");
           if (parameters[0].equals("repo")) {
               return ExecHelpers.exec(new String[]{"bash", "grade.sh", parameters[1]});
           }
           else {
               return "Couldn't find query parameter repo";
           }
       }
       else {
           return "Don't know how to handle that path!";
       }
    }
}

class GradeServer {
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

Server.java: 
```

import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;

import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

interface URLHandler {
    String handleRequest(URI url) throws IOException;
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
TestListExamples.java: 
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.Arrays;
import java.util.List;

class IsMoon implements StringChecker {
  public boolean checkString(String s) {
    return s.equalsIgnoreCase("moon");
  }
}

public class TestListExamples {
  @Test(timeout = 500)
  public void testMergeRightEnd() {
    List<String> left = Arrays.asList("a", "b", "c");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "c", "d");
    assertEquals(expected, merged);
  }

  @Test(timeout = 500)
  public void testMergeLeftEnd() {
    List<String> left = Arrays.asList("a", "b", "z");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "d", "z");
    assertEquals(expected, merged);
  }

  @Test(timeout = 500)
  public void testFilterSingle() {
    List<String> input = Arrays.asList("Moon", "MOO", "moo");
    List<String> expect = Arrays.asList("Moon");
    List<String> filtered = ListExamples.filter(input, new IsMoon());
    assertEquals(expect, filtered);
  }

  @Test(timeout = 500)
  public void testFilterMulti() {
    List<String> input = Arrays.asList("Moon", "MOO", "moon", "MOON");
    List<String> expect = Arrays.asList("Moon", "moon", "MOON");
    List<String> filtered = ListExamples.filter(input, new IsMoon());
    assertEquals(expect, filtered);
  }
}
```


- the full command line (or lines) you ran to trigger the bug:

bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-lab3 

- a description of what to edit to fix the bug:

Change ```git clone $0 student-submission``` to ```git clone $1 student-submission``` AND ```java -cp $CPATH org.junit.runner.JUnitCore > junit-output.txt``` to ```java -cp $CPATH org.junit.runner.JUnitCore TestListExamples> junit-output.txt``` 


# Part 2) Reflection 
One of the things I thought was interesting and had not seen before until the second half of this quarter would be bash scripts and working with Vim. I had not even seen the vim memes that the professor had mentioned. I still think it is a bit weird (like bash has odd if statements and uses square brackets instead of parentheses and vim is even MORE different!), but-- with practice-- I think it will be okay. I enjoyed lab and was really grateful to work with my partner, who was very encouraging and really made me feel like I could ask any questions.
