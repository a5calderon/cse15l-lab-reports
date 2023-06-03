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
- the contents of each file before fixing the bug 
- the full command line (or lines) you ran to trigger the bug 
- a description of what to edit to fix the bug 


# Part 2) Reflection 
- describe something you learned from you lab experience in second half of this quarter (a technical topic, something you learned from a tutor or classmate, etc)
