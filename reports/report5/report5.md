# Lab Report 5: Building on the Task in Lab Report 4

In this lab report, we will revisit the task we introduced in lab report 4. To refresh your memory, here are the set of tasks we attempted to do as fast as possible.

1) SETUP - Delete any existing forks of the repository you have on your account (if applicable)

2) SETUP - Fork the repository

3) Start the timer!

4) Log into ieng6

5) Clone your fork of the repository from your Github account

6) Run the tests, demonstrating that they fail

7) Edit the code file to fix the failing test

8) Run the tests, demonstrating that they now succeed

9) Commit and push the resulting change to your Github account

One of the rules of this challenge is that we could not use ```bash``` script so that we could practice working with command line shortcuts. But what if we removed this rule so that we could achieve the fastest possible speed? In this lab, we will remove all time from a human entering commands using a bash script.

To simplify the script, we will only include steps 4-9 in the script as these are the ones that are timed. To complete steps 1 and 2, refer to [Lab Report 4](https://rojiko1.github.io/cse15l-lab-reports/reports/report4/report4).

## Step 4

The first step will be to log into your ieng6 account using ```ssh```. Since 3-letter code for my code is ```agt```, my command for this step will be ```ssh cs15lwi23agt@ieng6.ucsd.edu```.

## Step 5

The next step is to clone your fork of the lab7 repository. The link can be found by clicking on ```<Code><ssh>``` on your repository page. For this step, my command will be ```git clone git@github.com:rojiko1/lab7.git```.

To be prepared for the next step, we will need to change our working directory to be inside the repository we just cloned. The command for this is ```cd lab7```.

## Step 6

The next step is to compile and run the JUnit tests to show that there is a bug in the code. The two commands to perform thi should be
```
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests
```

## Step 7

This step is to actually fix the bug in ListExamples.java. To do this step, we will have a corrected file already prepared in out ```ieng6``` account so that we can overwrite ListExamples.java to be identical to the corrected file.

In this case, my file, which I will name ```corrected.txt```, look like this:
```
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
    }
    return result;
  }


}
```

To actually utilize this corrected file, we will need this command: ```cat ../corrected.txt > ListExamples.java```.

> Note: In the command above, we use ```../``` because our working directory at the time of this command running is within ```lab7``` and the corrected file is outide of ```lab7```.

## Step 8

Next, we want to re-run the JUnit tests to show that the tests passed. Therefore, the commands will be identical to those in Step 6.

## Step 9

In this step, we will stage, commit, and push our changes. To stage our changes, we will use ```git add ListExamples```. To commit the changes, we will use ```git commit -m "fixed ListExamples.java"```. And lastly, to push the changes, we will use ```git push```.

## Putting It All Together

Now, we will put all of the steps together to create our bash script. But we must be careful, if we try to run our script from our local machine, which we will need to do in order to perform ```ssh```, the script will stop running as it will wait for the process on the remote machine to exit. To avoid this issue, we will have a crit on the local machine and one on the ```ieng6``` server. The script for your local machine should look like this:

```
ssh cs15lwi23agt@ieng6.ucsd.edu "bash run.sh"
```

> run.sh is the script on the ```ieng6``` server

Your remote script should look like this:

```
git clone git@github.com:rojiko1/lab7.git
cd lab7
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests
cat ../corrected.txt > ListExamples.java
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests
git add ListExamples.java
git commit -m "fixed ListExamples.java"
git push
```

## The Result

To prove that the bash script really is very fast, let's try running it and see what the time is. Less than 6 seconds! That is a lot faster than a human could ever achieve and shows us how useful it is to automate tasks.