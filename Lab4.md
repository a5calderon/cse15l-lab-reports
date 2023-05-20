# **Lab Report 4:  Doing it All from the Command Line**
---------
Task 1) Log into ieng6
![Image](https://github.com/a5calderon/cse15l-lab-reports/blob/main/Screen%20Shot%202023-05-19%20at%204.28.35%20PM.png)
For this step, I simply had to just do : ``` ssh cs15lsp23du@ieng6.ucsd.edu``` (and no password!).


Task 2) Clone your fork of the repository from your Github account
![Image](https://github.com/a5calderon/cse15l-lab-reports/blob/main/Screen%20Shot%202023-05-19%20at%204.28.56%20PM.png)
Like other times, I used ```git clone``` and the link from my repository. 

Task 3) Run the tests, demonstrating that they fail
![Image](https://github.com/a5calderon/cse15l-lab-reports/blob/main/Screen%20Shot%202023-05-19%20at%204.29.43%20PM.png)
After cloning, I checked where I was by using ```ls```. This reminded me to change the directory to lab7 ( which I did by ```cd lab7```. After this, I can use ```ls``` again to get a look at what is inside this directory. One thing I saw here was a bash file, so at this point I used ``` bash test.sh``` to run the J unit tests. After this, I saw that a test failed. 

Task 4) Edit the code file to fix the failing test
![Image](https://github.com/a5calderon/cse15l-lab-reports/blob/main/Screen%20Shot%202023-05-19%20at%204.30.49%20PM.png)
In order to get the tests to pass, I had to edit ListExamples.java. To do this all in the command line, I would have to use vim. Specifically, I typed : ```vim ListExamples.java```. After pressing enter, I was shown the contents of this file. In order to go to the specific spot that had an error, I just scrolled as far as I could (since the error was near the bottom)  and then used the ```<k>``` key 6 times to go up. Then, I used the <l> key until I was hovering the 1 in "index1". This was around 12 times. Next, I pressed ```<x>``` key, which removed the 1. I then pressed ```<i>``` key, in order to enter insert mode. After this, I inserted the number 2, as this would fix the error. I wanted to exit insert mode, so I pressed the ```<esc>``` key. Lastly, I wanted to save the changes so I typed ```;wq``` ( which saves and quits). 

Task 5) Run the tests, demonstrating that they now succeed
![Image](https://github.com/a5calderon/cse15l-lab-reports/blob/main/Screen%20Shot%202023-05-19%20at%204.31.20%20PM.png)
I was brought back to the terminal , so I decided to run the tests again ( by clicking on the up arrow twice) to confirm that was all that was wrong. The tests passed. 
  
Task 6) Commit and push the resulting change to your Github account (you can pick any commit message!)
![Image](https://github.com/a5calderon/cse15l-lab-reports/blob/main/Screen%20Shot%202023-05-19%20at%204.32.24%20PM.png)
I first did ```git status```, and this reminded me how to commit. So I ended up fowllowing the directions I got from there by doing ```git commmit -a```.  This brought me to this screen, so I added a quick little message (fixed!) and then saved (;wq). 
![Image](https://github.com/a5calderon/cse15l-lab-reports/blob/main/Screen%20Shot%202023-05-19%20at%204.32.48%20PM.png)
  Once again, I checked with ```git status``` to see what was left to do , and realized I forgot to push, so once again, following the instructions, I did ```git push```. This prompted my username and password for my github. After that was sorted out, I was able to see the changes on my github. 
![Image](https://github.com/a5calderon/cse15l-lab-reports/blob/main/Screen%20Shot%202023-05-19%20at%206.34.11%20PM.png)
