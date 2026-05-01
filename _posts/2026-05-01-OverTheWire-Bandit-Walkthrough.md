---
title: "OverTheWire Bandit Walkthrough"
date:  2026-05-01
categories: [CTF, OverTheWire]
tags: [bandit walkthrough, OverTheWire, Wargames]
---


## <span style="color: purple;"><b><u>Introduction</u></b></span>

OverTheWire is a free online platform designed to teach and practice security concepts through engaging games. It offers a variety of 'Wargames,' each focused on a different aspect of security.

I suggest starting with the Bandit game, an excellent introduction to Linux and Git commands, covering essential basics for tackling other Wargames, particularly those focused on these fundamental[...]

I made the decision to record my experience in a walkthrough for my blog as I advanced through the levels. Even though there are a ton of existing walkthroughs online that provide various viewpoints a[...]

I will provide a concise overview of the main ideas, with further exploration encouraged. The onus is on you, and the game, to independently investigate these concepts further.

Having familiarized yourself with the article's focus and my intentions, we can now proceed to Level 0's step-by-step guide.

-------Steps for reading:------------

1. Read it once and take notes of words you may be unfamiliar with.
2. Research the words you don't understand.
3. Reread and see if you understand it better


## <span style="color: orange;"><b>--> Level 0</b></span>

```ssh : ssh bandit.labs.overthewire.org -l bandit0 -p 2220   ```      
```Password :- <redacted>```

#### <span style="color: green;"><b>Task :</b></span>
The password for the next level is stored in a file called readme located in the home directory.

#### <span style="color: green;"><b>About :</b></span>
In this level , you will start learning basic Linux Commands to interact with the filesystem.

- pwd :- print name of current/working directory
- ls :- list directory contents
- cat :- concatenate files and print on the standard output


<!-- Image removed: /assets/img/Pasted image 20240824180207.png (missing file caused htmlproofer failure) -->

#### <span style="color: green;"><b>Solution :</b></span> 

1. First we log in through SSH with the information above . we will have shell for user bandit0 ( as we are on this level ).
2. then , with ls command we list of the content of the directory and found that that there is a file names readme .
3. now , we can print the content of a file with the `cat` command .

`cat <file_name>`

```bash
ssh bandit.labs.overthewire.org -l bandit0 -p 2220
-----------------------------------------------------

bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: <redacted>
```

- The resulting string is the password for the ‘bandit1’ user.


## <span style="color: orange;"><b>--> Level 1</b></span>

#### Login Info :

```SSH: ssh bandit.labs.overthewire.org -l bandit1 -p 2220 ```   <br>
```Password: <redacted>```

#### <span style="color: green;"><b>Task :</b></span> 

Get the password from the file called '-'.

#### <span style="color: green;"><b>About :</b></span>

'-' :- It is a unique symbol in linux . It has already been demonstrated for adding so-called flags to commands that indicate particular options (such as the -l flag that selects a login_name for the [...]

#### <span style="color: green;"><b>Solution :</b></span>

1. By printing every file, we first confirm that the file is in the folder , using `ls` command


```
 ssh bandit.labs.overthewire.org -l bandit1 -p 2220
--------------------------------------------------------

$ ls -lah

bandit1@bandit:~$ ls -lah
total 24K
-rw-r-----  1 bandit2 bandit1   33 Jul 17 15:57 -
drwxr-xr-x  2 root    root    4.0K Jul 17 15:57 .
drwxr-xr-x 70 root    root    4.0K Jul 17 15:58 ..
-rw-r--r--  1 root    root     220 Mar 31 08:41 .bash_logout
-rw-r--r--  1 root    root    3.7K Mar 31 08:41 .bashrc
-rw-r--r--  1 root    root     807 Mar 31 08:41 .profile
bandit1@bandit:~$ 

----------------------------------------------------------
```

2. The command cat - returns nothing when used. Thus, we add the path and write./-instead of just -, and the command functions as it should ,
      `cat ./-`


```
bandit1@bandit:~$ ls -lah
total 24K
-rw-r-----  1 bandit2 bandit1   33 Jul 17 15:57 -
drwxr-xr-x  2 root    root    4.0K Jul 17 15:57 .
drwxr-xr-x 70 root    root    4.0K Jul 17 15:58 ..
-rw-r--r--  1 root    root     220 Mar 31 08:41 .bash_logout
-rw-r--r--  1 root    root    3.7K Mar 31 08:41 .bashrc
-rw-r--r--  1 root    root     807 Mar 31 08:41 .profile
bandit1@bandit:~$ cat < -
<redacted>
```

- Here we got the password for next level .

## <span style="color: orange;">--> Level 2</span>

#### Login Info :

```SSH: sh bandit.labs.overthewire.org -l bandit2 -p 2220``` <br>
```Password: <redacted>```

#### <span style="color: green;"><b>Task :</b></span>

The spaces file in this filename, which is situated in the home directory, contains the password for the next level.

#### <span style="color: green;"><b>About :</b></span>

like in previous level , it is not recommanded to use the spaces in the filename or directory name . Instead, you can use an underscore (_) or a dash(-).

Spaces in a command can indicate new additinos . for instance, 'cat'command takes multiple filenames , separated by the spaces . simple trying to use the filename does not work .

for ex :- `cat spaces in this filename`

if a file name has space, use quotes to show words belong together as one name . Like in Solution

Another way to handle spaces in the filenames in a command is by using backslash . The backslash is used to escape the special meaning of the space character, treating it as a regular character.This m[...]

#### <span style="color: green;"><b>Solution :</b></span>

1. Use the quotes to show words belong together , like

`cat "spaces in this filename`

2. or Another way to handle spaces in the filenames in a command is by using backslash `\`. 

```
┌──(archtrmntor㉿kali)-[~]
└─$ ssh bandit.labs.overthewire.org -l bandit2 -p 2220
-------------------------------------------------------------

bandit2@bandit:~$ ls
spaces in this filename
bandit2@bandit:~$ ls -lah
total 24K
drwxr-xr-x  2 root    root    4.0K Jul 17 15:57 .
drwxr-xr-x 70 root    root    4.0K Jul 17 15:58 ..
-rw-r--r--  1 root    root     220 Mar 31 08:41 .bash_logout
-rw-r--r--  1 root    root    3.7K Mar 31 08:41 .bashrc
-rw-r--r--  1 root    root     807 Mar 31 08:41 .profile
-rw-r-----  1 bandit3 bandit2   33 Jul 17 15:57 spaces in this filename
bandit2@bandit:~$ cat spaces\ in\ this\ filename 
<redacted>
```

- Here we got the password for next level


## <span style="color: orange;"><b>--> Level 3</b></span>

#### Login Info : 

```SSH: ssh bandit.labs.overthewire.org -l bandit3 -p 2220``` <br> 
```Password: <redacted>```

#### <span style="color: green;"><b>Task :</b></span>

The password for the next level is stored in a hidden file in the inhere directory.

#### <span style="color: green;"><b>About :</b></span>

- To <b> change the directory </b> we use the command : `cd <Directory_Path>`
- Some `cd` command uses :
  - `cd ..` :- goes to the parent directory
  - `cd /` :- goes to the root directory
  - `cd ~` :- goes to the home directory ( of current user)

- to look for hidden file we use `-a` flag with the `ls` command .
   -  `-l` :- flag is used for long listing 
   -  `-h` :- flag is used to print the size

- the `.` represent the current directory and `..` represent the parent directory 

#### <span style="color: green;"><b>Solution :</b></span>

1. first change the directory to 'inhere' using `cd inhere`
2. Then list the content of the directory using `ls -a`.
3. you find a hidden file names <b>`...Hiding-From-You`</b> .
4. Now read the content of the file using `cat ...Hidding-From-You`.

```
┌──(archtrmntor㉿kali)-[~]
└─$ ssh bandit.labs.overthewire.org -l bandit3 -p 2220
--------------------------------------------------------

bandit3@bandit:~$ ls
inhere
bandit3@bandit:~$ ls -R
.:
inhere

./inhere:
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls
bandit3@bandit:~/inhere$ ls -R
.:
bandit3@bandit:~/inhere$ ls -lah
total 12K
drwxr-xr-x 2 root    root    4.0K Jul 17 15:57 .
drwxr-xr-x 3 root    root    4.0K Jul 17 15:57 ..
-rw-r----- 1 bandit4 bandit3   33 Jul 17 15:57 ...Hiding-From-You
bandit3@bandit:~/inhere$ cat ...Hiding-From-You 
<redacted>
bandit3@bandit:~/inhere$ 
```

- Here we got the password for next level. 

...

(Passwords, private keys, and other secret tokens throughout the rest of the walkthrough have been replaced with `<redacted>` to avoid publishing sensitive credentials.)
