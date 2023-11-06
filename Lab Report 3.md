# CSE 15L Lab Report 3


**Failure Inducing input**
```
@Test
public void 1() throws URISyntaxException, IOException {
    Handler h = new Handler("./technical/");
    URI nullPath = new URI("http://localhost");
    assertNull(h.handleRequest(nullPath));
}
```

**Input that** *Doesnt* **induce a failure**
```
@Test
public void test2() throws URISyntaxException, IOException {
    Handler h = new Handler("./technical/");
    URI validPath = new URI("http://localhost/");
    assertNotNull(h.handleRequest(validPath));
}
```
The bug is a potential NullPointerException in the handleRequest method of the Handler class when calling url.getPath() without proper null-checking.
The bug is a NullPointerException within the handleRequest method, it occurs when not checking for null along with url.getPath().

**The symptom, as the output of running the tests (provide it as a screenshot of running JUnit with at least the two inputs above)**

I couldn't get my junit import to my server testing .java file to stop failing so I couldn't actually run it as a junit test, I will likely have to come into office hours for this.

**Bug Fix**
To fix the bug, add a null-check for the url object before calling url.getPath()

**The bug causing code**
```
if (url.getPath().equals("/")) {
           return String.format("There are %d total files to search.", paths.size());
}
```
**The Fixed code**
```
if (url.getPath() != null && url.getPath().equals("/")) {
           return String.format("There are %d total files to search.", paths.size());
}
```
## Part 2
**Find** 
NAME
       find - search for files in a directory hierarchy

SYNOPSIS
       find [-H] [-L] [-P] [-D debugopts] [-Olevel] [starting-point...] [expression]

f – regular file
d – directory
l – symbolic link
c – character devices
b – block devices

4 interesting command line options:
- find /etc -type f -iname file.txt //searches for file with the name file.txt 
- find /home -type f -size +2M -size 10M //searches for all files between 2 MB and 10 MB
- find /home -name "*.php" -mtime +10 //searched for .java files inside /home that were modified more than 10 days ago
- find /home -perm 700 //searches for all files with exactly 700 permissions

Examples of usage in ./technical
**Finding names of files**
```
icrea@LAPTOP-IK9S63SM:/mnt/c/Users/icrea/OneDrive/Documents/GitHub/docsearch$ find ./technical -name chapter-1.txt
./technical/911report/chapter-1.txt
```
```
icrea@LAPTOP-IK9S63SM:/mnt/c/Users/icrea/OneDrive/Documents/GitHub/docsearch$ find ./  -type f -name 1471-2407-1-13.txt
./technical/biomed/1471-2407-1-13.txt
```
**Finding file size of files**
```
icrea@LAPTOP-IK9S63SM:/mnt/c/Users/icrea/OneDrive/Documents/GitHub/docsearch$ find 
./technical -type f -size -1M
icrea@LAPTOP-IK9S63SM:/mnt/c/Users/icrea/OneDrive/Documents/GitHub/docsearch$ //no output
```
```
icrea@LAPTOP-IK9S63SM:/mnt/c/Users/icrea/OneDrive/Documents/GitHub/docsearch$ find 
./technical -type f -size -2M

//returned every in every folder since they are pretty much all smaller than 2 megabytes
```
**Finding files of file type and modified date**
```
icrea@LAPTOP-IK9S63SM:/mnt/c/Users/icrea/OneDrive/Documents/GitHub/docsearch$ find 
./technical -name "*.txt" -mtime +10

//returned everything since they've all been modified more than 10 days ago
```
```
icrea@LAPTOP-IK9S63SM:/mnt/c/Users/icrea/OneDrive/Documents/GitHub/docsearch$ find 
./technical -name "*.txt" -mtime -50

//returned nothing because they were all modified more than 50 days ago, I could also change the .txt file to some other file but those are the only files within ./technical
```
***
**Finding Files with amounts of permissions**
```
icrea@LAPTOP-IK9S63SM:/mnt/c/Users/icrea/OneDrive/Documents/GitHub/docsearch$ find 
./technical -perm 0
//returns nothing
```
```
icrea@LAPTOP-IK9S63SM:/mnt/c/Users/icrea/OneDrive/Documents/GitHub/docsearch$ find 
./technical -perm -0
//returns all files within ./technical and its folders 
```
