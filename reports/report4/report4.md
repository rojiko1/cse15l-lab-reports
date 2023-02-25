# Lab Report 4: Terminal Efficiency

In this report, we have a challenge that is all about speed. Follow the instructions below and do the challenge as fast as you can. 

## Step 1

> If this is your first time trying the challenge, you can skip this step.

The first step is to delete any forks of the repository that you may have in your GitHub account. 

![Image](https://rojiko1.github.io/cse15l-lab-reports/assets/delete-fork-1)

While you are at it, delete the ```lab7``` directory from your ```ieng6``` account using the ```rm -rf lab7``` command.

![Image](https://rojiko1.github.io/cse15l-lab-reports/assets/delete-fork-2.png)

## Step 2

Next, fork the repository, which can be found here. Just click the ```Fork``` button, then click ```Create Fork```.

![Image](https://rojiko1.github.io/cse15l-lab-reports/assets/fork-repo.png)

## Step 3

Now, it time for the fun. Start the timer!

## Step 4

First, log into your ```ieng6``` account. I did this by simply hitting ```<up>```, then ```<Enter>```. I have created a SSH key so that I don't need to re-enter my password every time. As a result, I am already logged in and ready for the next step.

![Image](https://rojiko1.github.io/cse15l-lab-reports/assets/ieng6-login-no-pass.png)

## Step 5

Next, clone the repository that we forked earlier. For this, I used ```<up><up><up>``` then ```<Enter>``` to utilize a previous command I used. Before I did this, I made sure to ```cd``` into the directory that we created from cloning the repository. To ```cd```, I typed ```cd l``` then ```<Tab>``` and ```<Enter>```.

If this is your first time trying the challenge, find the link to your repository as shown.

![Image](https://rojiko1.github.io/cse15l-lab-reports/assets/lab7-git-clone-1.png)

This is what your git clone should look like:

![Image](https://rojiko1.github.io/cse15l-lab-reports/assets/klab7-git-clone-2.png)

## Step 6

For the next step, I copied and pasted the lines of code from [this link](https://ucsd-cse15l-w23.github.io/week/week3/), about half way down the page. Please note that you must use the Mac commands. I copied the ```javac``` command exactly but replaced ```ArrayTests``` with ```ListExamplesTests``` when running the ```java``` command. To make copying and pasting easier, I utilized ```<Ctrl> + <C>``` to copy and ```<Ctrl> + <V>``` to paste.

![Image](https://rojiko1.github.io/cse15l-lab-reports/assets/lab7-junit-tests-1.png)

## Step 7

Now to fix the bug, I opened the code in the terminal with the command ```nano ListExamples.java```. To fix the bug, I navigated down to line 42, column 13, using the ```<right>``` and ```<down>``` arrow keys. There, I hit ```<backspace>``` to remove the character ```1``` and replaced it with ```2```.

![Image](https://rojiko1.github.io/cse15l-lab-reports/assets/nano-lab7.png)

## Step 8

Now that the bug is fixed, we can re-run the tests. Since we did this in step 6 also, I used ```<up><up><up>``` then ```<enter>``` to re-run the ```javac``` command. Then, I used ```<up><up><up>``` then ```<enter>``` to re-run the ```java``` command. As expected, the tests now succeed.

![Image](https://rojiko1.github.io/cse15l-lab-reports/assets/lab7-junit-tests-2.png)

## Step 9

To commit and push the changes, I typed ```git add ListExamples.``` then ```<Tab><Enter>``` to run the ```git add ListExamples.java``` command, then ```git commit -m "fixed ListExamples"```, and last ```git push```.

![Image](https://rojiko1.github.io/cse15l-lab-reports/assets/lab7-git-add-commit-push.png)

And we're done. That took me a little over a minute. Try to beat my time. It is possible to do the task in less than a minute if you use more shortcuts or type faster than me. Good luck!