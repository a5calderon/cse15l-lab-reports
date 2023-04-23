# **Lab Report 2: Servers and Bugs**
---------

## Part One: StringServer

Code for StringServer:

 Screenshot # 1: using /add-message: 
 
 
 1) which methods in code are being called:
 2) what are the relevant arguments to those methods, and the values (Strings, ints, URIs) of any relevant fields of the class
 3) how do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.


 Screenshot # 2: using /add-message: 
 
 
 1) which methods in code are being called:
 2) what are the relevant arguments to those methods, and the values (Strings, ints, URIs) of any relevant fields of the class
 3) how do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.

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
