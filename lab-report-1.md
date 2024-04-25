# Using commands in Git Bash

**cd**

```
**no arguements**
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24/lecture1 (main)
$ cd

icrea@LAPTOP-IK9S63SM MINGW64 ~
$ 
```
Not an error, but it automatically reverts to the home directory, so the result would be a change in the working directory to the home directory. We can see this change when the "/OneDrive/Documents/CSE15LSP24/lecture1 (main)" disappears in the second line.

```
**path to a directory**
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24
$ cd lecture1/

icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24/lecture1 (main)
$
```
The result is a change in the Directory, now we are moved into a further directory of lecture1/ from inside its source working directory, "/OneDrive/Documents/CSE15LSP24/", I can now access this folder's contents directly.

```
**path to a file**
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24/lecture1 (main)
$ cd Hello.java 
bash: cd: Hello.java: Not a directory

icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24/lecture1 (main)
$
```
This was an error, it could not change directory to a file because the argument for cd must be a directory and in this case it is a file, thus causing an error.

**ls**

```
**no arguements**
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24
$ ls
lecture1/

icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24
$
```
This listed the only directory available (lecture1/) from the current directory we are in (~/CSE15LSP24).

```
**path to a directory**
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24
$ ls lecture1/
Hello.java  messages/  README

icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24
$
```
Here, there is now all the files and directories within the lecture1 folder/directory

```
**path to a file**
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24
$ ls lecture1/Hello.java
lecture1/Hello.java

icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24
$ cd lecture1/

icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24/lecture1 (main)
$ ls Hello.java
Hello.java

icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24/lecture1 (main)
$
```
When listing a file, the result will just be the arguement given, in this case "$ ls lecture1/Hello.java" resulted in "lecture1/Hello.java" and "$ ls Hello.java" resulted in "Hello.java"


**cat**

```
**no arguements**
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24
$ cat
[ctrl+c to exit]

icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24
$ cat
ls
ls
happy birthday!!  
happy birthday!!
[ctrl+c to exit]

icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24
$
```
This is not directly an error but rather a result of no input in a command that requires one to create an output, the output here will just print back whatever input is put in. However, since it isn't being used as intended there will be no usable results from using the command like this.

```
**path to a directory*
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24
$ cat lecture1/
cat: lecture1/: Is a directory

icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24
$
```
This is clarrifying that lecture1 is a directory and not a file. Since it's not a file, this will be the result.

```
**path to a file**
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24
$ cat lecture1/Hello.java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);
    System.out.println(content);
  }
}
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24
$
```
Here the cat command has output the entirety of the content in the file Hello.java, this is not an error but rather one of the primary purposes of this command.
