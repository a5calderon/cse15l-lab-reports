# **Lab Report 1: Remote Access and FileSystem**
---------

## **Step One: Installing VScode** 
To download VScode, open this [link](https://code.visualstudio.com). You will see this screen: 
![Image](https://raw.githubusercontent.com/a5calderon/cse15l-lab-reports/main/Screen%20Shot%202023-04-06%20at%204.34.41%20PM.png)

The next step is to click on the "download" button on the top right. Once you do that, you will see this. 
![Image](https://raw.githubusercontent.com/a5calderon/cse15l-lab-reports/main/Screen%20Shot%202023-04-06%20at%204.35.18%20PM.png)

From here, click on one of the following, depending on your type and model of your computer/laptop.
Now that it is downloaded, open it! It should look somewhat like this:

![Image](https://raw.githubusercontent.com/a5calderon/cse15l-lab-reports/main/Screen%20Shot%202023-04-06%20at%205.01.03%20PM.png)

## Step Two: Remotely Connecting 
FINDING THE TERMINAL: Under the "Start" heading, there's an option to create a new file. Click on that and name your file (make sure to add ".java" at the end). Next, open up the terminal (there's this button-- called the toggle panel--on the upper right that looks like a square that has a line through its lower 1/3). 

LOGGING IN: After finding the terminal, you should now be able to put in your course-specific account, which should look like this `$ ssh cs15lsp23zz@ieng6.ucsd.edu` (except that the zz is your uniquely assigned digits.After typing that in, you will be asked for your password.
![Image](https://raw.githubusercontent.com/a5calderon/cse15l-lab-reports/main/Screen%20Shot%202023-04-06%20at%205.14.45%20PM.png)
While it doesn't look like it's receiving your input (actually, it looks frozen), do not be alarmed. Just keep typing and press return once you are done. 
For those who have done this before, it should look like this: 
![Image](https://raw.githubusercontent.com/a5calderon/cse15l-lab-reports/main/Screen%20Shot%202023-04-06%20at%205.15.10%20PM.png)
Newcomers, however, will be presented with some text that states: `The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])? `
In this case, press yes. This will lead you to something like the image above.
And that's it ! You successfully connected your terminal to a computer in basement (the server). 
## Step Three:Trying Some Commands 
While there are many commands we CAN try, I am going to present here the ones I found most interesting. 
1. ls -a 
This looks like a list of files 
![Image](https://raw.githubusercontent.com/a5calderon/cse15l-lab-reports/main/Screen%20Shot%202023-04-06%20at%205.31.39%20PM.png)
3. cat /home/linux/ieng6/cs15lsp23/public/hello.txt
This outputs "Hello!", which was cool because I don't have a file that has this text on my end (so it just helped with the concept that I was connected to a computer in the basement). 
![Image](https://raw.githubusercontent.com/a5calderon/cse15l-lab-reports/main/Screen%20Shot%202023-04-06%20at%205.32.35%20PM.png)
5. ls /home/linux/ieng6/cs15lsp23/cs15lsp23zz, where the zz is one of the other group members’ username (my personal favorite) 
This one outputs permission denied! 
![Image](https://raw.githubusercontent.com/a5calderon/cse15l-lab-reports/main/Screen%20Shot%202023-04-06%20at%205.32.35%20PM.png)
