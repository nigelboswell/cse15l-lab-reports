# Today is **Friday**
- tomorrow will be Saturday
- the day after will be Sunday
- and the next will be Monday
  # Using commands in Terminal
**cd** (change directory)
'''
# no arguements
[user@sahara ~]$ cd
[user@sahara ~]$ 
'''
'''
# path to a directory
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$ 
'''
'''
# path to a file
[user@sahara ~/lecture1]$ cd Hello.java
bash: cd: Hello.java: Not a directory
'''
**ls** (list)
'''
# no arguements
[user@sahara ~]$ ls
lecture1
'''
'''
# path to a directory
[user@sahara ~]$ ls lecture1
Hello.class  Hello.java  messages  README
'''
'''
# path to a file
[user@sahara ~]$ ls lecture1/Hello.java
lecture1/Hello.java
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$ ls Hello.java
Hello.java
'''
**cat** (concatenate)
'''
# no arguements
[user@sahara ~]$ cat


no arguement
no arguement
'''
'''
# path to a directory
[user@sahara ~]$ cat lecture1
cat: lecture1: Is a directory
'''
'''
# path to a file
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
'''

