# Learn Linux
'''
Export IP=10.10.81.41
'''


# Task 1-2
Read the above

# Task 3 Section 1: SSH Intro

It may look intimidating at first, but you'll soon find out you can do much of the same functionality that you're able to do using graphical user interfaces!

It is an invaluable tool, and how you will be accessing this machine to learn and to do the challenges. Depending on the operating system there are different ways of SSHing into a machine. This section will purely focus on the windows way(PuTTY), and after we learn more about linux commands, and how they work, we'll return back to this section and learn about the linux method.

(No challenges)

# Task 4: Section 1: SSH - Putty and SSH)
Disclaimer: Please do not use instructions for putty if you are on a linux machine
	I suppose I cannot learn about putty then :(

SSH to shiba1@IP on port 22
	password: shiba1 

SSHing in completes the task

# Task 5: Section 2: Running Commands
On the machine, type echo hello

# Task 6: Section 2: Running Commands
1.  How would you output hello without a new line?
	echo -n hello

# Task 7: Section 3: Basic File Operations
1. hat flag outputs all entries?
	-a
2. What flag outputs things in a "long list" format?
	-l

# Task 8: Cat
1. What flag numbers all output lines?
	-n

# Task 9: Touch
	touch creates files

# Task 10: Running a binary
1. How would you run a binary called hello using the directory shortcut . ?
	./hello
2. How would you run a binary called hello in your home directory using the shortcut ~ ?
	~/hello
3. How would you run a binary called hello in the previous directory using the shortcut .. ?
	../hello

# Task 11: Shiba1
Create a file called noot.txt
Run the binary called shiba1 for the next password

1. What's the password for shiba2
	pinguftw

# Task 12: su
su allows you to change the user without logging out and whatnot
su on its own is equivalent to typing su root

# Section 4: Linux operators

command && command will run the second command after the first is successful

command & will start the command but bring up another prompt while it is running so you can keep doing stuff

  >> will append, as opposed to > which overwrites.

command; command will run the second command after the first regardless of if the first runs or not

# Section 5: Advanced file operators

When you do ls -l notice on the left of a file might have something like 
-rwxr-xr-x # root root

These are the file permissions, the owner, and the group that the file is in (skipping over the number)

| Value | Meaning                                        |
|-------|------------------------------------------------|
| 1     | That file can be executed                      |
| 2     | The file can be written to                     |
| 3     | The file can be executed and written to        |
| 4     | The file can be read                           |
| 5     | The file can be read and executed              |
| 6     | The file can be written to and read            |
| 7     | The file can be read, written to, and executed |

In the file permissions, the order is 
Owner, group, everyone else

Similar to CHMOD allowing you to change the permissions (first set of three), chown allows you to change the user and group, last two

chown user:group file
Or you can just use it to change the user


# Misc
## Adding users and groups
sudo adduser <name>
sudo addgroup <group>
usermod -a -G <groups seperated by commas> <user>

## Shebang! 
In the beginning of files meant to be executable, put 
#!/
i.e. 
#!/bin/bash/
#!/use/bin/env python3

## Processes
ps will show all user started process
ps -ef will show all running processes
	The second column is the PID
kill <PID>

top is the same as ps -ef except sorts by most resource consumption


# Directories!!
## /etc/passwd
	info on all users in the system
## /etc/shadow 
	Has the passwords of all the users
## /tmp
	Files in here are deleted on shutdown 
## /etc/sudoers
	Used to control the sudo permissions of every user on the system
## /root 
	Root users home directory
## /usr 
	Installed software
## /bin and /sbin
	All linux critical files
## /var
	Linux Misc directory, various things stored there
## $PATH 
	Environment variable with everything you are able to run (do echo $PATH, doing just $PATH will execute all of them)
## which
	Command that shows where an executable in the PATH variable is



