# Using commands in Git Bash

**cd**

```
**no arguements**
[icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24/lecture1 (main)] $ cd
[icrea@LAPTOP-IK9S63SM MINGW64 ~] $ 
```
Not an error, but it automatically reverts to the home directory, so the result would be a change in the working directory to the home directory. We can see this change when the "/OneDrive/Documents/CSE15LSP24/lecture1 (main)" disappears in the second line.

```
**path to a directory**
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$
```
The result is a change in the Directory, now we are moved into a further directory from the source, we can now access files directly from here

```
**path to a file**
[user@sahara ~/lecture1]$ cd Hello.java
bash: cd: Hello.java: Not a directory
```
This was an error, it could not change directory to a file because files are not directories

**ls**

```
**no arguements**
[user@sahara ~]$ ls
lecture1
```
This listed the only directory available from the current directory we are in

```
**path to a directory**
[user@sahara ~]$ ls lecture1
Hello.class  Hello.java  messages  README
```
Here there is now all the files and directories within the lecture1 folder/directory

```
**path to a file**
[user@sahara ~]$ ls lecture1/Hello.java
lecture1/Hello.java
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$ ls Hello.java
Hello.java
```
When listing a file, the result will just be the name of the file

**cat**

```
**no arguements**
[user@sahara ~]$ cat


no arguement
no arguement
```
I don't believe this is an error but rather a result of no input in a command that requires one to create an output,
the output here will just print back whatever input is put in

```
**path to a directory*
[user@sahara ~]$ cat lecture1
cat: lecture1: Is a directory
```
This is clarrifying that lecture1 is a directory and not a file. Since it's not a file, this will be the result

```
**path to a file**
[user@sahara ~]$ cat lecture1/Hello.java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8
);    
    System.out.println(content);
  }
```
Here the cat command has output the entirety of the content in the file Hello.java, this is not an error but rather one of the primary purposes of this command
