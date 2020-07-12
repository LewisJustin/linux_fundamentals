# Linux Challenge

# Users
'''
	garry:letmein
	bob:linuxrules
	alice:TryHackMe123
'''
'''
	mySQL
	root:hello
'''
## [Task 1]: Introduction
'''
This rooms purpose is to learn or improve your Linux skills.

There will be challenges that will involve you using the following commands and techniques:

    Using commands such as: ls, grep, cd, tail, head, curl, strings, tmux, find, locate, diff, tar, xxd
    Understanding cronjobs, MOTD's and system mounts
    SSH'ing to other users accounts using a password and private key
    Locating files on the system hidden in different directories
    Encoding methods (base64, hex)
    MySQL database interaction
    Using SCP to download a file
    Understanding Linux system paths and system variables
    Understanding file permissions
    Using RDP for a GUI
'''
1. No Answer Required

## [Task 2]: The Basics
'''
This set of tasks will go over the basic linux commands.

Each question might require you to switch between another user to find the answer!
'''

1. What is flag 1?
	Cat the file from garry's home directory
	f40dc0cff080ad38a6ba9a1c2c038b2c
'''
bob:linuxrules
'''

2. Log into bob's account using the credentials shown in flag 1.
   What is flag 2?
	Flag 1 displayed Bobs credentials.
	Cat flag 2
	f40dc0cff080ad38a6ba9a1c2c038b2c

3. Flag 3 is located where bob's bash history gets stored.
	cat .bash_history
	9daf3281745c2d75fc6e992ccfdedfcd

4. Flag 4 is located where cron jobs are created.
	crontab -e
	dcd5d1dcfac0578c99b7e7a6437827f3

5. Find and retrieve flag 5
	find / -name flag5.txt 2>/dev/null	
	cat /lib/terminfo/E/flag5.txt
	bd8f33216075e5ba07c9ed41261d1703

6. “Grep” through flag 6 and find the flag. The first 2 characters of the flag is c9
	find / -name flag6.txt 2>/dev/null
	grep c9 /home/flag6.txt
	c9e142a1e25b24a837b98db589b08be5

7. Look at the systems processes. What is flag 7
	ps -aef
	274adb75b337307bd57807c005

8. De-compress and get flag 8.
	tar -xzvf flag8.tar.gz
	cat flag8.txt
	75f5edb76fe98dd5fc9f577a3f5de9bc

9. By look in your hosts file, locate and retrieve flag 9.
	cat /etc/hosts
	dcf50ad844f9fe06339041ccc0d6e280

10. Find all other users on the system. What is flag 10.
	cat /etc/passwd
	5e23deecfe3a7292970ee48ff1b6d00

## [Task 3]: Linux Functionality
'''
Now we have used the basic Linux commands to find the first 10 flags, we will move onto using more functions that Linux has to offer.
'''
1. Run the command flag11. Locate where your command alias are stored and get flag 11.
	grep alias .bashrc
	b4ba05d85801f62c4c0d05d3a76432e0

2. Flag12 is located were MOTD's are usually found on an Ubuntu OS. What is flag12?
	ls /etc/update-motd.d/
	cat /etc/update-motd.d/00-header
	01687f0c5e63382f1c9cc783ad44ff7f

3. Find the difference between two script files to find flag 13
	find / -name flag13 2>/dev/null
	cd ../bob/flag13
	diff script1 script2
	3383f3771ba86b1ed9ab7fbf8abab531

4. Where on the file system are logs typically stored? Find flag 14.
	ls /var/log
	There's an interesting typo, I imagine they were trying to keep people from finding it
	cat /var/log/flagtourteen.txt
	71c3a8ad9752666275dadf62a93ef393

	Note to self: They made it so it would be the last thing displayed and therefore easy to find, however if it was hidden, you could have found it by sorting the file and looking for unique lines...

5. Can you find information about the system, such as the kernel version etc.
   Find flag 15.
	Google "how to find out what version of linux you are running
	cat /etc/os-release
	a914945a4b2b5e934ae06ad6f9c6be45

6. Flag 16 lies within another system mount.
	Ok so I was like ok, poke around in mount -l, turns out it is in /media
	ls /media
	ls /media/f
	ls /media/f/l
	...
	ls /media/f/l/a/g/1/6/is
	cab4b7cae33c87794d82efa1e7f834e6

7. Login to alice's account and get flag 17. Her password is TryHackMe123
'''
alice:TryHackMe123
'''
	su alice
		TryHackMe123
	cd ../alice
	cat flag17
	89d7bce9d0bab49e11e194b54a601362

8. Find the hidden flag 18.
	cat .flag18
	c6522bb26600d30254549b6574d2cef2

9. Read the 2345th line of the file that contains flag 19.
	cat -n flag19 | grep 2345
	490e69bd1bf3fc736cce9ff300653a3b

# [Task 4] Data Representation, Strings and Permissions
'''
This set of tasks will require you to understand how certain data is represented on a Linux system. This section may require you to do some independent research.
'''
1. Find and retrieve flag 20
	This is in alice's home directory
	cat flag20
	It is encoded apparently, with base 64
	base64 -d flag20 > flag20.txt
	02b9aab8a29970db08ec77ae425f6e68

2. Inspect the flag21.php file. Find the flag
	flag21.php is located in /home/bob
	cat flag21.php 
	<?='MoreToThisFileThanYouThink';?>
	cat -A flag21.php
	<?='$ POST[flag21_g00djob]'?>^M<?='MoreToThisFileThanYouThink';?>
	g00djob

3. Locate and read flag 22. Its represented as hex.
	cd ../alice
	Google hex to ascii to find xxd
	man xxd reveals -r to revert
	xxd -r flag22
	It is too short, back to the manual (also doesn't end with a new line, so add an empty echo)
	-p plain hexdump style
	xxd -r -p flag22 && echo
	9d1ae8d569c83e03d8a8f61568a0fa7d

4. Locate, read and reverse flag 23
	flag 23 is also in alice
	rev outputs the file backwords (from OTW)
	rev flag23
	ea52970566f4c090a7348b033852bff5

5. Analyse the flag 24 compiled C program. Find a command that might reveal human readable strings when looking in the source code.
	Finding flag 24
	find / -name flag24 2>/dev/null

	strings flag24 and look carefully through the output
	hidd3nSt1ng

6. Flag 25 DNE

7. Locate and retrieve flag 26.
Ok, after a massive amount of bumping around and coming up with a solution that would probably work with enough time
	find / -type f -print0 2>/dev/null | xargs -0 grep -E '^4bceb(.){27}$'
	4bceb76f490b24ed577d704c24d6955d
	xargs runs the command on everything passed to it. For some reason faster than just running grep directly?

8. Locate and retrieve flag 27, which is owned by the root user.
	find / -name flag27 -user root 2>/dev/null
	It is in /home/flag27
	We need root priveledges to do anything with it, so switch to alice
	sudo cat /home/flag27
	6fc0c805702baebb0ecc01ae9e5a0db5

9. What is the linux kernel version? 
	uname -a
	4.4.0–1075-aws

10. Find the file called flag 29 and do the following operations on it:
- Remove all spaces in file.
- Remove all new line spaces.
- Split by comma and get the last element in the split.

	found it in garry's home directory, cd /home/garry
	su garry: letmein
	cat flag29 | tr -d ' ' > flag29.1
	cat flag19.1 | tr -d '\n' > flag29.2
	cat flag29.2 | rev | cut -d ',' -f1 > backwards
	rev backwards
	fastidiisuscipitmeaei

# [Task 5] SQL, FTP, Groups and RDP
1. Use curl to find flag 30.
	curl localhost
	fe74bb12fe03c5d8dfc245bdd1eae13f
2. Flag 31 is a MySQL database name.
- MySQL username: root
- MySQL password: hello
	To login:
	mysql -u root -p
		> hello
	
	SHOW DATABASES;

3. Bonus flag question, get data out of the table from the database you found above!
	USE database_2fb1cab13bf5f4d61de3555430c917f4
	SHOW tables;
	SELECT * FROM flags;
	(where flags was a table as seen from show tables)

	ee5954ee1d4d94d61c2f823d7b9d733c

4. Using SCP, FileZilla or another FTP client download flag32.mp3 to reveal flag 32
	scp alice@10.10.187.194:/home/alice/flag32.mp3 .
	make sure everything is unmuted and listen
	tryhackme1337

5. Flag 33 is located where your personal $PATH’s are stored.
	su bob:linuxrules
	cd ../bob
	cat .profile
	547b6ceee3c5b997b625de99b044f5cf

6. Switch your account back to bob. Using system variables, what is flag34?
	printenv	
	7a88306309fe05070a7c5bb26a6b2def

7. Look at all groups created on the system. What is flag 35?
	cat /etc/group
	769afb6	
	or 
	getent group which yields the same result

8. Find the user which is apart of the “hacker” group and read flag 36
	Running groups as bob we find that we are the hacker, so we can cat /etc/flag36
	83d233f2ffa388e5f0b053848caed1eb
	we could have done groups alice, groups bob, etc until we found it but we were already the right use

9. Well done you've completed the linux CTF room
	no answer needed
