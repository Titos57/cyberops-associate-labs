# Lab 4.2.6 — Working with Text Files in the CLI

**Course:** Cisco CyberOps Associate
**Module:** 4.2.6
**Date:** March 2026
**Author:** Christos Panopoulos
**Tools Used:** SciTE, nano, nginx, Linux CLI

---

## Objective
Become familiar with Linux command-line text editors 
and configuration files using the CyberOps Workstation VM.

---

## Part 1 — Graphical Text Editor (SciTE)

### Opening SciTE and Creating a File
Opening the SciTE text editor can be done by typing `scite` on the terminal of the VM machine.
By adding the text required, we go to File > Save to give a name and save our text for future
usage.

![SciTE text file](../

### Finding Hidden Files
When trying to open a file with Scite, and it doesn´t show up, changing the dropdown area to 
All Files will start showing all the files and not just the extensions Scite is using by default.
In my case, looking for hidden configuration files that are represented by a dot(.) by default
on Linux distributions, didn´t show up by just changing the dropdown to All Files and
I had to use the CTRL + H shortcut to start viewing them.

---

## Part 2 — Command Line Text Editor (nano)

### nano Interface and Navigation
Files in a Linux distribution can also be accessed from the terminal with some built-in 
text editors. Having built-in text editors in the terminal can be especially useful, as
in the majority of time, remotely connecting to a server, with SSH, will not provide a GUI,
and the terminal is the only way of editing files.

In this lab, the nano text editor is used to modify the given file. Nano operates
entirely through keyboard shortcuts that can be seen at the bottom of the terminal
when using nano, including shortcuts such CTRL+X to exit, CTRL+O to save, and CTRL+G for help.
When lines extend beyond the visible screen boundary in nano, a `>` character can be seen
at the end of the line.

![nano text editor](../

---

## Part 3 — Working with Configuration Files

### Step 1 — Locating Configuration Files
Configuration files start with a dot(.) in front of them. Every
application in Linux systems runs according to one or more configuration files that 
specify how the application will run. Such files are grouped by default at the
/home directory for the current user's personal configuration files and at /etc, where
system-wide configuration files are located with limited or no access to modification
for standard users without root privileges. This security architecture that Linux applies to
the /etc directory prevents unauthorized modification of system services, limiting the blast
radius of a compromised user account.

### Step 2 — Editing .bashrc
In this lab, we locate and edit the .bashrc file, which is responsible for the terminal
view. By editing the file by either scite or nano and changing the line PS1='\[\e[1;32m\]
from 32 to 31, turns the terminal name color from green to red. Changes to the configuration
files usually do not take effect until the session is refreshed.

![Red name text](../

### Step 3 — Editing nginx Configuration
Now moving to the /etc directory and modifying a service like nginx. The nginx web server 
configuration file was edited using nano with sudo privileges, as the file is stored in /etc 
and requires root permissions to modify. Two changes were made to custom_server.conf: the 
listening port was changed from 81 to 8080, and the web root directory was updated 
to /usr/share/nginx/html/text_ed_lab/.

After saving the configuration and starting nginx with the modified file, navigating to
127.0.0.1:8080 in Firefox successfully loaded the lab confirmation page, verifying 
that the configuration changes took effect immediately.

---

## Key Observation
This lab demonstrated that in Linux, every application and service operates based on 
predefined rules set in configuration files. Configuration files spread between directories
like /home and /etc ensure safety from unauthorized users modifying critical system services.
Understanding how configuration files work as a SOC analyst is essential because detecting 
unauthorized changes in such files during an incident is crucial.









