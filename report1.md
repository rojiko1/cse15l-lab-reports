# Lab 1: Logging into a Course-Specific Account on ```ieng6```

## Install Microsoft Visual Studio Code

Before logging into your course-specific account, it is important that you first have a terminal open to run commands remotely. I used VSCode as my terminal, which you can download [here](https://code.visualstudio.com/). I already have VSCode installed so I will skip this step.

Once you have VSCode installed and open, click on ```Terminal -> New Terminal``` in the menu.

![Image](https://rojiko1.github.io/cse15l-lab-reports/vscode-terminal-newterminal.png)

## Access Your ```ieng6``` Account

The first step of logging into your account will be looking up your account [here](https://sdacs.ucsd.edu/~icc/index.php). If you are a new student or have not set up your account yet, you will need to set your password. Simply look for the prompt and follow the directions. Note that the password change can take up to 15 minutes to take effect.

If you are on Windows, there is an additional step, which is to install Git [here](https://gitforwindows.org/). I already have Git installed so I will skip this step.

To connect to the remote server start by using the following command, replacing ```abc``` with your specific letters in your account.

```
ssh cs15lwi23abc@ieng6.ucsd.edu
```

If you see a message that looks like this, just type ```yes``` to proceed with the connection process.

```
The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

You will now be prompted to enter your password. Note that as you are entering your account password, it may appear as though the terminal is not recording what you are typing even though it actually is. When you complete this step, your terminal should look something like this:

![Image](https://rojiko1.github.io/cse15l-lab-reports/remote-connection-terminal.png)

## Play Around With Some Commands

Now that you're set up, it is time to use some commands to play around with the remote server's file system.

Here are some commands you can try:

```cd``` - change your working directory
```ls``` - list your current directory. Some options to use with ```ls``` include ```-l```, ```-a```, and ```-t```.
```pwd``` - print your working directory
```mkdir``` - make a new directory
```cp``` - copy a file or directory or create a new file or directory

For some inspiration, here are some things that I tried:

![Image](https://rojiko1.github.io/cse15l-lab-reports/terminal-commands-1.png)

![Image](https://rojiko1.github.io/cse15l-lab-reports/terminal-commands-2.png)

When you are down trying out different commands, run the ```exit``` command to disconnect from the remote server.
