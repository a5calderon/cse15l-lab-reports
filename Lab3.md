# **Lab Report 3: Researching Commands**
---------

## Part One: Picking a command: find 
---------
## Part Two: 4 interesting command-line options/ ways to use the command

1) First command line option: find /path/to/directory -name "filename"
    
    Examples(codeblock of command and output): 
    

```
andreac@Andreas-MacBook-Pro stringsearch-data % find technical/biomed -name "rr196.txt"
technical/biomed/rr196.txt
```
```
andreac@Andreas-MacBook-Pro stringsearch-data % find technical/biomed -name "rr196"    
```

source: terminal manual

Explanation: I chose to do find because I was a little confused during lecture how to use the -name command line option of find. After researching it a bit, I now know that it is exactly how it seems/reads. It searches for a file ,within a given directory, with a specified name (the text that was inside the quotes). If there was no file with the exact name, it returns nothing. This is shown in the second example.This is a helpful trick, especially if you have a lot of files.  


---------
2) Second command line option: find /path/to/directory -type d

 Example 1 (codeblock of command and output): 
  
  ```
andreac@Andreas-MacBook-Pro stringsearch-data % find technical -type d
technical
technical/government
technical/government/About_LSC
technical/government/Env_Prot_Agen
technical/government/Alcohol_Problems
technical/government/Gen_Account_Office
technical/government/Post_Rate_Comm
technical/government/Media
technical/plos
technical/biomed
technical/911report
```
 
  Example 2 (codeblock of command and output):
  ```
andreac@Andreas-MacBook-Pro stringsearch-data % find technical/biomed -type d
technical/biomed
  ```
    
Explanation: This command line option outputs all the possible directories within a specficied directory. In the first example, the specified directory was "technical", and this output an actual list. However, the second example was technical/biomed , which does not have any other directories within it (just files). As a result, the only directory it gave me was the technical/biomed. This reminds me of ls, only formatted differently (and more conveniently)-- as a result, this may be a useful, quick alternative. 
    
Source:ChatGPT, after asking it "what are some useful "find" commands"
    
3) Third command line option: find /path/to/directory -name "*.txt" -print
    
    Example 1 (codeblock of command and output): 

``` 

    andreac@Andreas-MacBook-Pro stringsearch-data % find technical/biomed -name "1472*" -print
technical/biomed/1472-6807-2-2.txt
technical/biomed/1472-6750-3-11.txt
technical/biomed/1472-6882-3-3.txt
technical/biomed/1472-6807-2-3.txt
technical/biomed/1472-6807-2-1.txt
technical/biomed/1472-6947-3-8.txt
technical/biomed/1472-6890-2-5.txt
technical/biomed/1472-6963-2-10.txt
technical/biomed/1472-6769-1-4.txt
technical/biomed/1472-6882-3-1.txt
technical/biomed/1472-6785-1-3.txt
technical/biomed/1472-6831-2-2.txt
technical/biomed/1472-6807-2-4.txt
technical/biomed/1472-6750-1-12.txt
technical/biomed/1472-6904-2-7.txt
technical/biomed/1472-6882-1-7.txt
technical/biomed/1472-6874-2-1.txt
technical/biomed/1472-6793-2-8.txt
technical/biomed/1472-6769-1-1.txt
technical/biomed/1472-6750-1-13.txt
technical/biomed/1472-6920-1-3.txt
technical/biomed/1472-6807-2-5.txt
technical/biomed/1472-6904-2-4.txt
technical/biomed/1472-6750-1-11.txt
technical/biomed/1472-6769-1-3.txt
technical/biomed/1472-6769-1-2.txt
technical/biomed/1472-6904-2-5.txt
technical/biomed/1472-6823-3-1.txt
technical/biomed/1472-6785-1-5.txt
technical/biomed/1472-6807-3-1.txt
technical/biomed/1472-6750-1-8.txt
technical/biomed/1472-6890-1-4.txt
technical/biomed/1472-6904-3-1.txt
technical/biomed/1472-6793-2-16.txt
technical/biomed/1472-6807-3-2.txt
technical/biomed/1472-6904-1-2.txt
technical/biomed/1472-6831-3-1.txt
technical/biomed/1472-6793-2-17.txt
technical/biomed/1472-6807-1-1.txt
technical/biomed/1472-6874-3-2.txt
technical/biomed/1472-6785-2-6.txt
technical/biomed/1472-6920-2-3.txt
technical/biomed/1472-6815-2-3.txt
technical/biomed/1472-6785-2-7.txt
technical/biomed/1472-6890-3-2.txt
technical/biomed/1472-6793-1-8.txt
technical/biomed/1472-6750-2-21.txt
technical/biomed/1472-6882-2-10.txt
technical/biomed/1472-6882-2-5.txt
technical/biomed/1472-6963-1-8.txt
technical/biomed/1472-6920-2-1.txt
technical/biomed/1472-6793-2-11.txt
technical/biomed/1472-6823-2-2.txt
technical/biomed/1472-6750-2-13.txt
technical/biomed/1472-6793-1-6.txt
technical/biomed/1472-6793-3-4.txt
technical/biomed/1472-6963-3-11.txt
technical/biomed/1472-6963-3-6.txt
technical/biomed/1472-6874-2-13.txt
technical/biomed/1472-684X-2-1.txt
technical/biomed/1472-6963-3-7.txt
technical/biomed/1472-6793-3-5.txt
technical/biomed/1472-6750-2-10.txt
technical/biomed/1472-6963-3-12.txt
technical/biomed/1472-684X-2-2.txt
technical/biomed/1472-6793-3-6.txt
technical/biomed/1472-6963-3-13.txt
technical/biomed/1472-6750-3-4.txt
technical/biomed/1472-6750-1-6.txt
technical/biomed/1472-6947-2-7.txt
technical/biomed/1472-6963-3-1.txt
technical/biomed/1472-6793-3-3.txt
technical/biomed/1472-6750-2-14.txt
technical/biomed/1472-6963-3-14.txt
technical/biomed/1472-6963-1-11.txt
technical/biomed/1472-6793-2-19.txt
technical/biomed/1472-6947-2-4.txt
technical/biomed/1472-6793-2-18.txt
technical/biomed/1472-6750-3-6.txt
technical/biomed/1472-6793-1-2.txt
technical/biomed/1472-6882-1-10.txt
technical/biomed/1472-6793-1-12.txt
technical/biomed/1472-6882-1-11.txt
technical/biomed/1472-6793-2-4.txt
technical/biomed/1472-6750-2-2.txt
technical/biomed/1472-6793-1-11.txt
technical/biomed/1472-6793-2-5.txt
technical/biomed/1472-6947-1-2.txt
technical/biomed/1472-6882-1-12.txt
technical/biomed/1472-6807-2-9.txt
technical/biomed/1472-6955-2-1.txt
technical/biomed/1472-6947-1-6.txt
technical/biomed/1472-6793-2-1.txt
technical/biomed/1472-6874-2-8.txt
technical/biomed/1472-6793-1-15.txt
technical/biomed/1472-6947-3-5.txt
technical/biomed/1472-6947-1-5.txt
technical/biomed/1472-6793-2-2.txt
technical/biomed/1472-684X-1-5.txt
  ```

  
Example 2 (codeblock of command and output):

```
andreac@Andreas-MacBook-Pro stringsearch-data % find technical/911report -name "chapter" -print
andreac@Andreas-MacBook-Pro stringsearch-data % find technical/911report -name "chapter*" -print
technical/911report/chapter-13.4.txt
technical/911report/chapter-13.5.txt
technical/911report/chapter-13.1.txt
technical/911report/chapter-13.2.txt
technical/911report/chapter-13.3.txt
technical/911report/chapter-3.txt
technical/911report/chapter-2.txt
technical/911report/chapter-1.txt
technical/911report/chapter-5.txt
technical/911report/chapter-6.txt
technical/911report/chapter-7.txt
technical/911report/chapter-9.txt
technical/911report/chapter-8.txt
technical/911report/chapter-12.txt
technical/911report/chapter-10.txt
technical/911report/chapter-11.txt
andreac@Andreas-MacBook-Pro stringsearch-data % find technical/911report -name "chapter*" -print0
technical/911report/chapter-13.4.txttechnical/911report/chapter-13.5.txttechnical/911report/chapter-13.1.txttechnical/911report/chapter-13.2.txttechnical/911report/chapter-13.3.txttechnical/911report/chapter-3.txttechnical/911report/chapter-2.txttechnical/911report/chapter-1.txttechnical/911report/chapter-5.txttechnical/911report/chapter-6.txttechnical/911report/chapter-7.txttechnical/911report/chapter-9.txttechnical/911report/chapter-8.txttechnical/911report/chapter-12.txttechnical/911report/chapter-10.txttechnical/911report/chapter-11.txt%

```

    
What is it doing and why is it helpful: This, to me, looked exactly like just doing the same command without the "-print". I'm guessing that in earlier times, the command line without print would actually not print (and that over the years the print just became a default). So, I tried looking for things to do with print, and found -print0. The difference is that it no longer prints the files on different (new) lines or with spaces between the file names . I think it is nice to have options. In the examples, I showed that you can place the asterisk in the end (not just the beginning--which is what was seen in lecture). In addition, the command needs it to be specfic or at least have an asterisk. It is not enough to have part of a name, without an asterisk. 
    
Source: ChatGPT, after asking it "what are some useful "find" commands"
   
4) Fourth command line option: find /path/to/directory -name "*.txt" -delete

    Example 1 (codeblock of command and output): 
    
  ```
  andreac@Andreas-MacBook-Pro stringsearch-data % find technical/911report -name "chapter*" -print0 > myFile.txt
  andreac@Andreas-MacBook-Pro stringsearch-data % find myFile.txt -delete
  ```

    
  Example 2 (codeblock of command and output):
  
 ```
 andreac@Andreas-MacBook-Pro stringsearch-data % find technical/911report -name "chapter*" -print0 > myFile.txt
andreac@Andreas-MacBook-Pro stringsearch-data % find *File.txt -delete
andreac@Andreas-MacBook-Pro stringsearch-data % find technical/911report -name "chapter*" -print0 > myFile.txt
andreac@Andreas-MacBook-Pro stringsearch-data % find "*File.txt" -delete 
find: *File.txt: No such file or directory
 ```
  
What is it doing and why is it helpful: This searches for the file you specified and then deletes it. This is useful for when you have a long list of files, and cannot find one particular one you want to delete. In the example, I tried to show that I wasnt able to use quotation marks for this command option, but still could use and asterisk. 
    
Source: terminal manual  
