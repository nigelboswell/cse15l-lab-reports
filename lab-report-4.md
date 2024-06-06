# Lab Report 4

## Steps 1-3:
These steps are mostly irrelevant to this report and involve setting up my personal fork of the lab 7 repository, deleting previous versions of this repository, and setting up an ssh key for my ieng6 account to access my Github account.

## Step 4: SSH login to ieng6
**Screenshot:**
![image](https://github.com/nigelboswell/cse15l-lab-reports/assets/146788276/505ab928-2f39-4740-9fed-b7d21acbc552)

**Commands and Key presses:**
```
ssh nbsowell@ieng6.ucsd.edu
Pressed: s s h <Space> n b o s w e l l @ i e n g 6 . u c s d . e d u <Enter>
```
This input command connects my local computer to the school ieng6-202 remote server. Since I already have a set up rsa-ID key I have no need to input any password to connect to the server from my local machine.

## Step 5: Clone my fork of the repository from my Github account 
**Screenshot:**
![image](https://github.com/nigelboswell/cse15l-lab-reports/assets/146788276/7360cba5-06bc-48f9-b4ce-ccf555b516f8)

**Commands and Key presses:**
```
git clone git@github.com:nigelboswell/lab7.git
Pressed: g i t <Space> c l o n e <Space> <Ctrl + v> <Enter>
```
Now this command clones my ssh version of my forked lab7 repository. The <Ctrl + v> pastes the "git@github.com:nigelboswell/lab7.git" from my local clipboard to the command line.

## Step 6: Complie, Run tests, Demonstrate Failure
**Screenshot:**
![image](https://github.com/nigelboswell/cse15l-lab-reports/assets/146788276/0f2b071e-02fa-409d-83e7-f5b9912ceb8d)

**Commands and Key presses:**
Command 1:
```
cd lab7
Presses: c d <Space> l a b 7 <Enter>
```
This command changes directory into the new /lab7 repo that we cloned in the previous step.

Command 2:
```
javac -cp .:"lib/*" ListExamplesTests.java
Presses: j a v a <Space> - c p <Space> . : " l i b / * " <Space> o r g . j u n i t . r u n n e r . J U n i t C o r e <Space> L i s t E x a m p l e s T e s t s <Enter>
```
This command compiles the java Test file contents of the lab7, in this case it applies specifically to the ListExamplesTests.java file. If there were any critical errors in the code they would appear after this command, since it just retrutned the command line, it is safe to assume that we can run the code with no major errors.

Command 3:
```
java -cp .:"lib/*" org.junit.runner.JUnitCore ListExamplesTests
Presses: j a v a <Space> - c p <Space> . : " l i b / * " <Space> o r g . j u n i t . r u n n e r . J U n i t C o r e <Space> L i s t E x a m p l e s T e s t s <Enter>
```
This runs the ListExamplesTests.java file and the tests within it. As expected, we see one of the tests have failed resulting in a failure of one of the methods in the ListsExamples.java file. From the output: ..E we know that the second test failed due to the 1st dot being the succesful run of the test with a successive dot for the start of test 2 followed by an E, meaning that the following or second test has failed/resulted in error.

## Step 7: Edit and Fix Code
**Screenshots:**
![image](https://github.com/nigelboswell/cse15l-lab-reports/assets/146788276/f0afa162-af20-4934-a7e4-9c3203b30c8c)
![image](https://github.com/nigelboswell/cse15l-lab-reports/assets/146788276/34b746e7-b1e2-4fc8-85b6-dab103995209)
![image](https://github.com/nigelboswell/cse15l-lab-reports/assets/146788276/2bd8da93-6760-490d-8f1f-2f1b90950d84)

**Commands and Key presses:**
Command 1:
```
vim ListExamples.java
Pressed: v i m Space L i s t E x a m p l e s . j a v a <Enter>
```
Commands Key Presses in Vim:
```
:44
Pressed: : 4 4 <Enter>
```
This brings my cursor to line 44, the source of the problem, we must turn the index1 on this line to index2
```
e r 2
Pressed: e r 2
```
e brings my cursor to the end of the current word, in this case onto the 1 in index1, r is the replace input, this will replace whatever character is below the cursor with the next character I input, with this in mind I press 2, replacing the 1 in index1 to a 2 making it index2.
```
:wq
Pressed: : w q <Enter>
```
This exists vim while saving my edits to the file.

## Step 8: Compile, Run Tests, Demonstrate Success
**Screenshot:**
![image](https://github.com/nigelboswell/cse15l-lab-reports/assets/146788276/08547729-dbcb-4509-8617-6389a601894a)

**Commands and Key presses:**
Command 1:
```
javac -cp .:"lib/*" ListExamplesTests.java
Pressed: <up> <up> <up> <Enter>
```
The previous 3 comamnds in order were: 
```
vim ListExamples.java
java -cp .:"lib/*" org.junit.runner.JUnitCore ListExamplesTests
javac -cp .:"lib/*" ListExamplesTests.java
```
By pressing up arrow 3 times this brings up the javac -cp .:"lib/*" ListExamplesTests.java command, pressing enter after this runs it.
Command 2:
```
java -cp .:"lib/*" org.junit.runner.JUnitCore ListExamplesTests
Pressed: <up> <up> <up> <Enter>
```
Same concept as the last command, since we ran one more command, our third most recent command was java -cp .:"lib/*" org.junit.runner.JUnitCore ListExamplesTests, so we press up arrow 3 times and then enter to run.

As we can see after running these commands the Java test files compile with no error and run with no error. This means our edit in vim was a success and our code works without error now.

## Step 9: Commit and push the resulting change to my Github account
**Screenshot:**
![image](https://github.com/nigelboswell/cse15l-lab-reports/assets/146788276/811a17dc-dd12-4c13-a185-4462a4a79d8b)

**Commands and Key presses:**
Command 1:
```
git add .
Pressed: g i t <Space> a d d <Space> . <Enter>
```
This command adds all current files to my clipboard of what I will eventually push into my main repository that I cloned earlier.
Command 2:
```
git commit -m "Fix error index1 to index 2"
Pressed: g i t <Space> c o m m i t <Space> - m <Space> " F i x <Space> e r r o r <Space> i n d e x 1 <Space> t o <space> i n d e x 2 " <Enter>
```
This command takes my added files to a commit with the following message "Fix error index1 to index 2"
Command 3:
```
git push
Pressed: g i t <Space> p u s h <Enter>
```
This takes my commit and it's message and pushes the changes in all the selected files to the original cloned repository on my Github.

## Conclusion: 
This lab report has taught me the intricacies of Vim as a tool and it's ability to work along with SSH-ing and Git editing.
