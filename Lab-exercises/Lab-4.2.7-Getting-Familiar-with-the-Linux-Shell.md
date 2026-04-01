# Lab 4.2.7 — Getting Familiar with the Linux Shell

**Course:** Cisco CyberOps Associate  
**Category:** Practical / Hands-On  
**Platform:** CyberOps Workstation Virtual Machine (Linux)  
**Date Completed:** April 2026

---

## Objective
In this lab, the goal is to develop proficiency with the command line and learn 
basic and important terminal commands, such as `man`, `pwd`, `cd`, `cp`, `mv`, and `rm`, as
well as output redirection `>`, `>>` that every Linux user, and especially a SOC analyst or 
a penetration tester should know how to enumerate through system files while investigating.

---

## Part 1: Shell Basics

### Step 1: Access the Command Line
When launching the terminal by clicking the terminal window on the dock, critical information is
displayed - the user´s name and the machine name are shown, as well as the specific directory 
the terminal is accessing, and a symbol `$`, which indicates the user´s privileges in that case
those of a standard user, if the symbol is `#`, this indicates we are connected as root or superuser.

![Terminal Window of analyst](../Lab-screenshots/Linux%20Commands/terminal.png)

---

### Step 2: Display Manual Pages
It is critical to know the way to find more information about a command. By using the `man` command
and the specific command for which more information is required, a user can find out the description,
synopsis, examples, overview, defaults, and options for the specific command.

Using the man command, an analyst can retrieve information about critical commands like,
the `pwd` command, which is responsible for printing the working directory, and the `cp` command
which is used to copy files and directories to other locations on the machine. Having knowledge
about the man command to find information about any command you encounter during an investigation
is key for a SOC analyst.

![Information about the cp command](../Lab-screenshots/Linux%20Commands/man%20cp.png)

---

### Step 3: Create and Change Directories
Creating directories in a Linux environment can be done by using the `mkdir` command
and specifying the name of the directory a user wants to create. The directory will be created in
the current directory that the user is in, which can be found with the `pwd` command.

Changing between directories can be done with `cd` and the specific directory or path the user
wants to move to. The user can see the available directories that they can change with either
`ls -l` command or `ls -la`, which also displays the hidden directories with the dot(.) in 
front. With `cd`, a user can move to the home directory by typing `cd ~` or move a directory
back with `cd ..`. Navigation as a SOC analyst in a Linux environment is the most crucial 
skill for any investigation.

![ls command run](../Lab-screenshots/Linux%20Commands/ls%20command.png)
![ls -la command run](../Lab-screenshots/Linux%20Commands/ls%20-la%20command.png)

---

### Step 4: Redirect Outputs
Redirecting output from run commands can be a great way of saving the results into a text file 
helping an analyst come back to review in a later stage of an investigation. This can be done 
by using the `>` symbol, which creates or overwrites the specified file. For example, 
man ls > some_text.txt will redirect the results of the man command from the terminal to the 
file some_text.txt; if the file some_text.txt doesn´t exist, it will be created
or if it does, everything in it will be overwritten by the new text without any warning.

![redirecting an echo command](../Lab-screenshots/Linux%20Commands/Redirect.png)

---

### Step 5: Redirect and Append to a Text File
The `>>` symbol in comparison to `>`, redirects and appends to the existing file. A text
file will not be overwritten when using `>>` as it will append to the file the new redirected
text, as seen when run with the cat command, which prints the contents of a file. Such 
redirection is used for logs that need to contain both past and present information, where
using `>` will overwrite all the past text that was logged, losing crucial evidence for
an investigation.

![appending to a file](../Lab-screenshots/Linux%20Commands/Appending.png)

---

### Step 6: Work with Hidden Files
Checking the amount of directories on the home directory reveals 40 directories. By 
using the command `ls -la`, a wider range of 136 files is revealed, those files are called the
hidden directories. Most of the hidden files contain configuration settings on how a
specific user's application will work, such as .bashrc, .profile, or even the history of commands
run in a user's terminal, .bash_history.

![ls -l output](../Lab-screenshots/Linux%20Commands/ls%20-%20l%20output.png)
![ls -la output](../Lab-screenshots/Linux%20Commands/ls%20-la%20output.png)

---

## Part 2: Copying, Deleting, and Moving Files

### Step 1: Copying Files
Copying files in a Linux distribution can be done with the `cp` command. The `cp` command
is used by specifying the source (file to copy) and the destination (where the copied
file will be placed). In contrast to the `mv` command, where you move a source from
one location to another, the `cp` command creates a copy of the original file and 
places it in the destination, leaving the original file intact. In a SOC analyst
investigation, the analyst would always work with a copied file to preserve the integrity
of the evidence.

![cp command and verification](../Lab-screenshots/Linux%20Commands/cp%20command.png)

---

### Step 2: Deleting Files and Directories
Removing files and directories in a Linux environment is done by the `rm` command.
The `rm` command deletes the file or directory specified by the user. Deleting a 
directory requires the `rm -r` command, which is necessary, as `-r` specifies to the terminal
to delete everything inside the directory.

Using commands in Linux like `rm` is permanent and cannot be undone, so a user
needs to be aware and careful while using them. Commands like `rm -r` are also used
by malware to delete any traces of its actions.

---

### Step 3: Moving Files and Directories
Moving files is done by the `mv` command. Using the `mv` command, a user needs
to specify the source and the destination, if a user wants a file to be moved in 
its current directory, the `.` symbol can be used at the destination. The `mv` command
is different from the `cp` command, as it moves the file by removing it from its original
location and placing it in the new location. Attackers may use the `mv` command to move
malware around a machine to avoid detection.

![Moving file to current directory](../Lab-screenshots/Linux%20Commands/mv%20command.png)

---

## Key Observations
As a professional in the field of security, having Linux CLI proficiency is an essential competancy.
Using commands like `rm`, `mv`, `>>`, and `ls` is necessary to navigate through Linux
and conduct any investigation as a SOC analyst. In a real-world breach scenario, an analyst
would use the `ls -la` command to uncover hidden malware traces, `>>` to build investigation logs, and
`.bash_history` hidden file to reconstruct the attacker's actions during the breach.

