# **Lab Report 2: Servers and Bugs**
---------

## Part One: StringServer

Code for StringServer:
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

class Handler implements URLHandler {
   String running=""; 
   public String handleRequest(URI url) {
    if (url.getPath().contains("/add-message")) {
       // System.out.println("url after contains:" +url); //
        String[] parameters = url.getQuery().split("=");
       // System.out.println("parameters[0]:" +parameters[0]);
       // System.out.println("parameters[1]:" +parameters[1]);
        running= running +"\n" + parameters[1];
        return running;
    }else {
        return "welcome! use this framework ' /add-message?s=<string> ' to add strings to a running list:)"; 
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


 Screenshots: using /add-message: 

 ![Image](https://raw.githubusercontent.com/a5calderon/cse15l-lab-reports/main/Screen%20Shot%202023-04-23%20at%202.08.45%20PM.png)
 
 1) which methods in code are being called:


 On the right, ``` java StringServer 1759``` calls the main method.

 2) what are the relevant arguments to those methods, and the values (Strings, ints, URIs) of any relevant fields of the class:


This creates the port by using the user’s array of numbers (an argument for the main method). 
 
 4) How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.


Once the user opens the link, they are met with a screen with the text "welcome! use this framework ' /add-message?s=<string> ' to add strings to a running list:)" , which makes sense because the current url is simply  ```http://localhost:1759```  . It currently does not contain "/add-message"


---------
	
 ```http://localhost:1759/add-message?s=hi``` :
	
 ![Image](https://raw.githubusercontent.com/a5calderon/cse15l-lab-reports/main/Screen%20Shot%202023-04-23%20at%202.09.53%20PM.png)
 
 1) which methods in code are being called:
	
This calls the handRequest method again. This method’s argument is a URI url. 

 2) what are the relevant arguments to those methods, and the values (Strings, ints, URIs) of any relevant fields of the class
	
This URI url now contains “/add-message?s=hi”. Because of this, the condition for the ‘if block’ is met. Inside the if statement, the url is split into two (between the equals sign) and the 2 strings are placed in an array (that was created inside the if statement) called parameters. We are now able to add to the running string that was created outside of the if statement by updating running to include “\n” and the current second element in the parameters array. Lastly, we return the “running” string. In this case, parameters=[/add-message?s, hi].


 3) how do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.

 And because running is currently an empty string returns simply ```\n hi``` (of course the \n is not visible).
	
---------

```http://localhost:1759/add-message?s=hey``` :
	
![Image](https://raw.githubusercontent.com/a5calderon/cse15l-lab-reports/main/Screen%20Shot%202023-04-23%20at%202.10.03%20PM.png)

1) which methods in code are being called:
	
This calls the handRequest method again. 

2) what are the relevant arguments to those methods, and the values (Strings, ints, URIs) of any relevant fields of the class
	
This method’s argument is a URI url. This URI url now contains “/add-message?s=hey”. In this case, parameters=[/add-message?s, hey].

3)how do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
	
	
The string “running” is not empty, so it was crucial to make sure  it updates the values instead of rewriting running (running=running +”\n” + parameters[1]). As a result, running now is 
	
```
\n hi 
\n hey
```
	
---------
	
```http://localhost:1759/add-message?s=hello there``` : 
	
![Image](https://raw.githubusercontent.com/a5calderon/cse15l-lab-reports/main/Screen%20Shot%202023-04-23%20at%202.10.12%20PM.png)
 
In this case,  parameters=[/add-message?s, hello there] and running now is 
	
```
\n hi 
\n hey
\n hello there
```
	
---------
	
## Part Two:One bug from lab 3 : ReverseInPlace

A failure-inducing input for the buggy program (as a J unit test):
	
```
@Test 
public void testReverseInPlaceWithLongerList() {
    int[] input1 = { 1, 2, 3}; //failure inducing input 
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3, 2, 1}, input1  );// actual: {3,2,3}

  }
@Test   
public void testReverseInPlaceWithLongererList() {
    int[] input1 = { 1, 2, 3, 4}; //failure inducing input 
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 4, 3, 2, 1}, input1 );// actual: {4,3,3,4}
	}
	
  ```
	
Any input that doesn't induce a failure (as a Junit test):
	
```
@Test 
public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);//expected, actual
	}
 ```

The symptom, as the output of running the tests:
	
![Image](https://raw.githubusercontent.com/a5calderon/cse15l-lab-reports/main/Screen%20Shot%202023-04-23%20at%201.03.47%20PM.png)

The bug (before changes and after changes) :

BEFORE:
	
```
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
  ```
				  
AFTER:
				  
```
 // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp= arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }
```

EXPLAINATION : 
In the original code, inside the for loop,   there was no temporary variable to store a number at a specific index before that number was overwritten with a different number. For example, in the array {1,2,3}--> the 3 can be placed at index 0, but once that action is committed, the 1 is overwritten and thus cannot be placed at index 2. Instead the current value at index 0 would be placed at index 2 (which was the number 3). Thus, without a temporary variable, this would result in {3,2,3}. However, there is still more work to do. In the condition section in the 'for loop', we see that the loop's condition for it to be executed is for i to be less than the length of the array. We would have to cut this in half, in order to actual see the array be reversed (without cutting it in half  {1,2,3} would still be {1,2,3}.
## Part Three: Reflection

One thing I learned from lab week 2 was how to create/work with a server. At first, I was very intimitated and it did take me a while to understand sections of code. For example, working with URLs in methods was new to me, so I had to put print statements throughout the code to see what is going on (like printing out the url code in each 'if statement' block and after the url was split up). Another thing that was new to me was this line of code: 
```Server.start(port, new Handler()); ```
It takes in the port (which would be the random number the user picked and the handler method created. 
