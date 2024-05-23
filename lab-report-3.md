# Lab Report 3

## Part 1: Bugs


### A Failure-Inducing Input for the Buggy Program as a JUnit Test:

Below is a Junit test which induces a program failure. The program fails beacuse the reversing of the array results in failure where there are an even number of elements within the input array

```
 @Test 
  public void testReverseInPlace2() {
      int[] input1 = { 5, 4 };
      ArrayExamples.reverseInPlace(input1);
      assertArrayEquals(new int[]{ 4, 5 }, input1);
  }
```
## An Input That Doesn't Induce a Failure as a JUnit Test:

Below is a JUnit test which passes and does not induce a failure. The input is a single element, something somewhat easy to account for

```
 @Test 
  public void testReverseInPlace() {
      int[] input1 = { 3 };
      ArrayExamples.reverseInPlace(input1);
      assertArrayEquals(new int[]{ 3 }, input1);
  }
```

This updated test presents a scenario where the program functions correctly, dealing with an array containing an odd number of elements.

```
@Test 
public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
}
```
### The Symptom

The image below provides the output of our tests, here we see a failure due to the testReverseInPlace2() test not succeeding
![image](https://github.com/nigelboswell/cse15l-lab-reports/assets/146788276/883a54e2-694f-4742-b22e-afb4cd198cb6)


### Debug

Given Code:
```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

The given method reverses the array, however it replaces elements instead of assigning temp variables and swapping, resulting in failure for practically all inputs other than 1 element arrays. It also runs the whole length of the array which will attempt to reverse the array twice which is an additional failure

New Code:

The corrected code fixes the bug by properly swapping elements from both ends towards the center, ensuring accurate reversal for arrays of any size.

```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length / 2; i++) {
    int temp = arr[i];
    arr[i] = arr[arr.length - i - 1];
    arr[arr.length - i - 1] = temp;
  }
}
```
### Why the Fix Addresses the Issue

This fix solves the problems stated prior in which the array would swap the elements twice, and also overwrite elements. It accommplishes this by iterating until halfway through the length of the array and also by assigning the variables for swapping to a temp variable first, then swapping. These two fixes ensure that as it iterates through the first half of the array, it swaps the elements opposite of the current index relative to the middle point of the array. These changes ensure correct swapping given any length of array

![image](https://github.com/nigelboswell/cse15l-lab-reports/assets/146788276/d0928164-6e3d-4717-acf7-3a9a9bfc9390)



## Part 2

### The **Find** Commad

According to Source: https://man7.org/linux/man-pages/man1/find.1.html we have the following:
(Source: https://man7.org/linux/man-pages/man1/find.1.html)
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

###Examples of usage in ./technical

**Finding names of files** 

Example 1:
```
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24/workinglabreport3/docsearch (main)
$ find ./technical -name chapter-1.txt
./technical/911report/chapter-1.txt
```

Example 2: 
```
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24/workinglabreport3/docsearch (main)
$ find ./  -type f -name 1471-2407-1-13.txt
./technical/biomed/1471-2407-1-13.txt
```
This is recursively rsearching through the technical folder for instances of files with the name "chapter-1.txt" This can be useful for finding specific files within a repository. (Source: https://man7.org/linux/man-pages/man1/find.1.html)


**Finding file size of files**

Example 1:
```
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24/workinglabreport3/docsearch (main)
$ find ./technical -type f -size -1M
```
The above command resulted in no output since there is no file smaller than 1 megabyte

Example 2:
```
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24/workinglabreport3/docsearch (main)
$ find ./technical -type f -size -2M
```
This version of the command resulted in the returning of virutally all files within the technical repository since that practically all are less than 2 megabyte

This command searches for files smaller than the set size at the end, in the examples above the M stands for Megabytes and the number preceeding it is the ammount of megabytes. This is useful for finding files of specific sizes. (Source: https://man7.org/linux/man-pages/man1/find.1.html)


**Finding files of file type and modified date**

Example 1:
```
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24/workinglabreport3/docsearch (main)
$ find ./technical -name "*.txt" -mtime +10
```
This returned nothing, meaning all .txt files were modified within the last 10 days, this is due to me just recently cloning and downloading them

Example 2:
```
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24/workinglabreport3/docsearch (main)
$ find ./technical -name "*.txt" -mtime -50
```
This resulted in returning everything since all files in the repository were modified within the last 50 days since I just recently cloned and downloaded them

This command searches recurssively for files with parameters of date last modified where the number is the ammount of days and the (+/-) are over and under ammount of time respectively. This can be useful for seeing things such as recently changed or modified files. (Source: https://man7.org/linux/man-pages/man1/find.1.html)


**Finding Files with amounts of permissions**

Example 1:
```
icrea@LAPTOP-IK9S63SM MINGW64 ~/OneDrive/Documents/CSE15LSP24/workinglabreport3/docsearch (main)
$ find ./technical -perm 0
```
This returns nothing as there are no files with permissions set to 0

Example 2:
```
icrea@LAPTOP-IK9S63SM:/mnt/c/Users/icrea/OneDrive/Documents/GitHub/docsearch$ find 
./technical -perm -0
```
This returns all files within ./technical repository as it is essentially a general search for all files in the repository

This command searches recurssively for files in the repository under the parameters of their assigned permission bits. More specifically, for example 1 (- perm (mode)) acording to my source: 
"File's permission bits are exactly mode (octal or symbolic).  Since an exact match is required, if you want to use this form for symbolic modes, you may have to specify a rather complex mode string.  For example `-perm g=w' will only match files which have mode 0020 (that is, ones for which group write permission is the only permission set)."
This differs from the Example 2 (-perm -(mode)) where the -(mode) searches broadly for the bits mode that are set for the file. In Example 2 specifically, the -0 is pratically an open parameter since all files within the repo are under a basic permission. (Source: https://man7.org/linux/man-pages/man1/find.1.html)


