# Lab Report 5

## Part 1: Debugging Scenerio

**An Orignal Post From Student Looking For Help On Piazza:**
Summary: 
Java program incorrect result error
Details: 
Hello,
I am having issues with my Java program that checks if a file exists given a directory. however, I am getting an unexpected output.
Here is my code:
```java
import java.io.File;

public class Exists {
   public static void main(String[] args) {
       File file = new File(args[0]);
       if (file.exists()) {
           System.out.println("This File exists");
       }
       else {
           System.out.println("This file does not exist");
       }
   }
}
```
Here is my directory:
-Parent Directory
  - src
    - java
      - Exists.class
      - Exists.java
  - files
    - textDocuments
      -WarAndPeace.txt 

```bash
PS C:\Users\icrea\Parent Directory\src\java> java Exists files/textDocuments/WarAndPeace.txt
This file does not exist
```
As seen above when I run: java Exists files/textDocuments/WarAndPeace.txt I get This file does not exist even though it does. Please HELP!


**TA response to the post:**
Hi,

I believe your problem lies in the directory that you are running your java file in.
Most likely the current directory that you are running Exists.java from is not able to back-track to the input directory give.
To solve this try either editing your program to account for the full path directory where the java file is first, then in your code, search the absolute path to the file from there. 
Hopefully this helps! Please reply if you have any other problems.

**Student applying the solution**
Hi,

To fix the error I added the following line of code after main(String[] args){ and before File file = new File(args[0])):
String dir = Paths.get("").toAbsolutePath().toString(); 
then for the argument of new File() I changed it to (dir, args[0]).
The code now accounts for the parent directory of the Exists.java file, then it searches in this directory for the input path of the file.
My new result is:
```bash
PS C:\Users\icrea\Parent Directory\src\java> java Exists files/textDocuments/WarAndPeace.txt
The File exists
```
Which is the expected result. THANK YOU!

# Summary of Scenerio and Solution
A common problem for many porgrams is forgetting to account for the path or directory of the program and the other files it is attempting to access.
In this scenerio we see that the student was trying to access a .txt file using their java file but both files were in completely different working paths.
This is the code pre-fix:
```java
import java.io.File;

public class Exists {
   public static void main(String[] args) {
       File file = new File(args[0]);
       if (file.exists()) {
           System.out.println("This File exists");
       }
       else {
           System.out.println("This file does not exist");
       }
   }
}
```
This is the output of the code:
```bash
PS C:\Users\icrea\Parent Directory\src\java> java Exists files/textDocuments/WarAndPeace.txt
This file does not exist
```

Here is the code post-fix:
```java
import java.io.File;

public class Exists {
   public static void main(String[] args) {
       String dir = Paths.get("").toAbsolutePath().toString();
       File file = new File(dir, args[0]);
       if (file.exists()) {
           System.out.println("This File exists");
       }
       else {
           System.out.println("This file does not exist");
       }
   }
}
```
This is the updated output of the code post-fix:
```bash
PS C:\Users\icrea\Parent Directory\src\java> java Exists files/textDocuments/WarAndPeace.txt
The File exists
```
To solve this solution in the future, make sure to account for different directories and absolute pathing.
By using a line of code as the one use here where it finds the absolute path then searches from there, we can ensure this error is prevented.

## Part 2: Reflection
Within the second half of this quarter the labs have taught me a lot about autograding, testing, and debugging code. As I've progressed through this courseload I've been made very much aware of the importance of fixcing faulty code and preventing basic errors through means of tests.
I also enjoyed learning about the importance of AI in lecture as a tool going forward in the world and the world of Computer Sceince. 
