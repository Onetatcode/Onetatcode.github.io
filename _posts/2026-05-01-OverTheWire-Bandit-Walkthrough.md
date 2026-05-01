---
title: "OverTheWire Bandit Walkthrough"
date:  2026-05-01
categories: [CTF, OverTheWire]
tags: [bandit walkthrough, OverTheWire, Wargames]
---


## <span style="color: purple;"><b><u>Introduction</u></b></span>

OverTheWire is a free online platform designed to teach and practice security concepts through engaging games. It offers a variety of 'Wargames,' each focused on a different aspect of security.

I suggest starting with the Bandit game, an excellent introduction to Linux and Git commands, covering essential basics for tackling other Wargames, particularly those focused on these fundamental ski[...]

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


![Level-0](/assets/img/Pasted image 20240824180207.png)

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


## <span style="color: orange;"><b>--> Level 4</b></span> 

#### Login Info :

```SSH: ssh bandit.labs.overthewire.org -l bandit4 -p 2220``` <br>
```Password:- <redacted>```

#### <span style="color: green;"><b>Task :</b></span> 

The password for the next level is stored in the only human-readable file in the inhere directory.

#### <span style="color: green;"><b>About :</b></span>

The `file` command give us the type of data of the file is . Some example would be like : 'txt', 'ruby',exe',ASCII text, etc .

Here in this task we are looking for the human-redable file and ELF file is not human-readable. The most common data encoding that are humar redable are ASCII and Unicode . 

we can use the `*` wildcard with the `file` command , this wildcard stand for any number of literal or character  ,it can also be used to select 'everything' in one . Here's how we do it 

#### <span style="color: green;"><b>Solution :</b></span>

-  First change directory to the 'inhere' directory .
-  Second , we can read each and every file one by one so we use the wildcard to get the type of all the files , using command : `file ./*`


```
|──(archtrmntor㉿kali)-[~]
└─$ ssh bandit.labs.overthewire.org -l bandit4 -p 2220
--------------------------------------------------------

bandit4@bandit:~/inhere$ ls
-file00  -file02  -file04  -file06  -file08
-file01  -file03  -file05  -file07  -file09
bandit4@bandit:~/inhere$ cat < -file07
<redacted>
bandit4@bandit:~/inhere$ cat < -file08
<redacted>
                   ы�Ϣ��bandit4@bandit:~/inhere$ 
```

-  we can see that only <b>'-file07'</b> is of type 'ASCII test'.
-  Now we can read the content of the file using: `cat ./-file07`

```
bandit4@bandit:~/inhere$ file ./*

./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```

- Here we got the password for next level.

## <span style="color: orange;"><b>--> Level 5</b></span>

#### Login Info :

```SSH:  ssh bandit.labs.overthewire.org -l bandit5 -p 2220``` <br>
```Password: <redacted>```

#### <span style="color: green;"><b>Task :</b></span>


The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

- human-readable
- 1033 bytes in size
- not executable

#### <span style="color: green;"><b>About :</b></span>

`find` command is used for searching and locating file or directories within a file system based on a specific crietria such as name,type,date,execution,size,ownership etc. with designated flag .

`grep` command searches its input for lines containing a specific pattern defined by th user . It can also be used to do the opposite, meaning when using the `-v` flag , a line witha defined pattern w[...]

Some flag usages of `find` command:
    - `-size` is used to looking at file size in bytes.
    - `-type f` is used to look at files.
    - `-readable` flag , mean you have the permission to read the files .
    - Instead , we could use `-exec <command>` flag with `{}` as a path, meaning the chosen command will be executed on all the files. This could be used to execute another command like `file`.

#### <span style="color: green;"><b>Solution :</b></span>

1. Change the directory to <b>'inhere'</b> .
2. we have to find the file who have
    - `-size 1033`
    - `-type f`
    - `-exec file '{}' \;` , to execute the file command and get the file data type .and then we need to grep the <b>ASCII'</b> as file type . 
3. Then we read the file content to get the password for next level . 


```
┌──(archtrmntor㉿kali)-[~]
└─$ ssh bandit.labs.overthewire.org -l bandit5 -p 2220
----------------------------------------------------------

bandit5@bandit:~/inhere$ find . -type f -size 1033c ! -executable -exec file '{}' \; | grep ASCII

./maybehere07/.file2: ASCII text, with very long lines
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
<redacted>
```

- Here we got the password for next level.

## <span style="color: orange;"><b>--> Level 6</b></span>


#### <span style="color: green;"><b>Login Info :</b></span>

```SSH: ssh bandit.labs.overthewire.org -l bandit6 -p 2220``` <br>
```Password: <redacted>```


#### <span style="color: green;"><b>Task :</b></span>

The password for the next level is stored **somewhere on the server** and has all of the following properties:

- owned by user bandit7
- owned by group bandit6
- 33 bytes in size


#### <span style="color: green;"><b>About :</b></span>

Here the main topic is File Permission , Specially to the area of the ownership > each and every file is ownmed by a user and a group . we can see this information using the `ls` command with `-l` fla[...]

we can also combine it with the find command to search through , specific detail  of the file using 
    - `-user` :- flag to specify the user 
    - `-group` :- to specify the group 
    - `-size` :- to specify the size 


#### <span style="color: green;"><b>Solution :</b></span>

1. use the command `find` with specific flag , we can lcoate the exact file we are searching for 

Command :- `find / -user bandit7 -group bandit6 -size 33c 2>/dev/null`

- `Here 2>/dev/null` :- syntax in Linux is used to redirect error output to the null device, effectively discarding it. This is useful when you want to run a command without seeing error messages. The[...]


```
┌──(archtrmntor㉿kali)-[~]
└─$ ssh bandit.labs.overthewire.org -l bandit6 -p 2220
-----------------------------------------------------------

bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
<redacted>
bandit6@bandit:~$ 
```

- Here we got the password for the next level.

## <span style="color: Orange;"><b>--> Level 7</b></span>

#### <span style="color: green;"><b>Login Info :</b></span>

```SSH: ssh bandit.labs.overthewire.org -l bandit7 -p 2220 ``` <br>
```Passwd: <redacted>```

#### <span style="color: green;"><b>Task :</b></span>

The password for the next level is stored in the file **data.txt** next to the word **millionth**

#### <span style="color: green;"><b>About :</b></span>

`grep` command is used to serch lines for specific patter using : `grep <Pattern>`.
with the '(|)' , we can pipe the output of cat to grep as input to look through a text file . 

#### <span style="color: green;"><b>Solution :</b></span>

1. first list out the content in the directory using `ls`.
2. Second  , we can pipe the output of `cat` to `grep` to look for string **millionth** , next to which is our passsword  

```
┌──(archtrmntor㉿kali)-[~]
└─$ ssh bandit.labs.overthewire.org -l bandit7 -p 2220
-----------------------------------------------------------

bandit7@bandit:~$ ls
data.txt
bandit7@bandit:~$ cat data.txt | grep millionth
millionth	<redacted>
bandit7@bandit:~$ 
```

- Here we got the password for the next level . 

## <span style="color: orange;"><b>--> Level 8</b><span>


#### <span style="color: green;"><b>Login Info :</b></span>

```SSH: ssh bandit.labs.overthewire.org -l bandit8 -p 2220``` <br> 
```Password: <redacted>```

#### <span style="color: green;"><b>Task :</b></span>

The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once

#### <span style="color: green;"><b>About :</b></span>

`sort` : Sorting is necessary because the `uniq` command works on consecutive duplicate lines.

The `sort` command arranges the lines in order, so identical lines appear consecutively or in the ascending order . By Default , it sorts lexicographically ( i.e, alphabetically )
- The `uniq -u` command is used to filter out unique lines from the sorted input > it only print the lines that are not repeated . 


#### <span style="color: green;"><b>Solution :</b></span>

1. First list out the content of the directory using the `ls` command , then 
2. sort the data using the sorted command , 
3. then with the help of piping `|` character that passed the output of the previous command as input to the next command , then 
4. use the `uniq -u` to filter out unique lines from the sorted input . 

Command : `sort data.txt | uniq -u `


```
┌──(archtrmntor㉿kali)-[~]
└─$ ssh bandit.labs.overthewire.org -l bandit8 -p 2220
-----------------------------------------------------------

bandit8@bandit:~$ sort data.txt | uniq -u
<redacted>
bandit8@bandit:~$ 
```

- Here we got the password for the next level .

## <span style="color: orange;"><b>--> Level 9</b></span>

#### <span style="color: green;"><b>Login Info :</b></span>

```SSH: ssh bandit.labs.overthewire.org -l bandit9 -p 2220``` <br>
```Password: <redacted>```
\
#### <span style="color: green;"><b>Task :</b></span>

The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.

#### <span style="color: green;"><b>About :</b></span>

`strings` command finds the human-redable strings in files. It prints printable character sequences specifically. It is mostly used for non-printable files, such as executables or hex dumps.

#### <span style="color: green;"><b>Solution :</b></span>

1. first list out the content of the directory ,
2. then use the `strings` command with the `grep` command to extrac th several `===` strings form the `data.txt` file we have given .

Command : `strings data.txt | grep ===`

```
┌──(archtrmntor㉿kali)-[~]
└─$ ssh bandit.labs.overthewire.org -l bandit9 -p 2220
-----------------------------------------------------------

bandit9@bandit:~$ strings data.txt | grep ===
\a!;========== the
========== passwordf
========== isc
========== <redacted>
bandit9@bandit:~$ 

```

- Here we got the password for the next level.


## <span style="color: orange;"><b>--> Level 10</b></span>

#### <span style="color: green;"><b>Login Info :</b></span>

```SSH: ssh bandit.labs.overthewire.org -l bandit10 -p 2220``` <br>
```Password: <redacted>```


#### <span style="color: green;"><b>Task :</b></span>


The password for the next level is stored in the file **data.txt**, which contains base64 encoded data


#### <span style="color: green;"><b>About :</b></span>

1. base64 is a binary-to-text encoded scheme. it is usually by the equal sign in the end of the data , but not always . In Linux has a command named `base64` that allows encoding and decoding in `base[...]

#### <span style="color: green;"><b>Solution :</b></span>

1. First list out the content of the directory , 
2. then use the `base64` command to decode the data from the text file .

Command : `base64 -d data.txt`

```
┌──(archtrmntor㉿kali)-[~]
└─$ ssh bandit.labs.overthewire.org -l bandit10 -p 2220
-----------------------------------------------------------

bandit10@bandit:~$ base64 -d data.txt 
The password is <redacted>
bandit10@bandit:~$ cat data.txt 
<redacted>
bandit10@bandit:~$ 
```

- Here we got the password for the next level.


## <span style="color: orange;"><b>--> Level 11</b></span>

#### <span style="color: green;"><b>Login Info :</b></span>

```SSH: ssh bandit.labs.overthewire.org -l bandit11 -p 2220``` <br>
```Password: <redacted>```

#### <span style="color: green;"><b>Task :</b></span>

The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

#### <span style="color: green;"><b>About :</b></span>

rotation by 13 is basically the **ROT13** substitution cipher . Substition means replacing one character with another . 
In Linux `tr` command means `translate` that allows replacing characters with others . Here its syntax looks like `tr <old_chars> <new_chars>`

tr 'A-Za-z' 'N-ZA-Mn-za-m'`: This command tells `tr` to replace each uppercase letter (A-Z) with the letter 13 positions ahead (N-Z followed by A-M) and each lowercase letter (a-z) with the correspond[...]

#### <span style="color: green;"><b>Solution :</b></span>

-  First , this can solved with the online tool names [cyberchef](https://gchq.github.io/CyberChef/) , and selecting **ROT13** as cooking . 

[Cyber chef solution](https://gchq.github.io/CyberChef/#recipe=ROT13(true,true,false,13)&input=R3VyIGNuZmZqYmVxIHZmIDdrMTZKQXJVVnY1THhWdUpmc1NWZGJidGFIR2x3OUQ0Cg)

or 

-  for **ROT13** we have to do `A->N` and `Z->M` , with `tr` commads looks like :

Command :- `tr 'A-Za-a' 'N-ZA-Mn-za-m'`

-  we have to use this with piping character with `cat` , that inputs the data of 'data.txt' to `tr`.

```
┌──(archtrmntor㉿kali)-[~]
└─$ ssh bandit.labs.overthewire.org -l bandit11 -p 2220
-----------------------------------------------------------

bandit11@bandit:~$ cat data.txt 
Gur cnffjbeq vf <redacted>
bandit11@bandit:~$ tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
The password is <redacted>
bandit11@bandit:~$ 
```
- here we got the password for next level .


## <span style="color: orange;"><b>--> Level 12</b></span>


#### <span style="color: green;"><b>Login Info :</b></span>

```SSH: ssh bandit.labs.overthewire.org -l bandit12 -p 2220``` <br>
```Password: <redacted>```

#### <span style="color: green;"><b>Task :</b></span>

The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp [...]

#### <span style="color: green;"><b>About :</b></span>

`file` command is used to determine the type of a file . The command examines the files and make a guess based on its content or magic numbers , and then return the file type . For example , `file tex[...]

1. `tar`: This is a tape archiving utility in Unix and Unix-like operating systems. It's used to collect multiple files into a single tarball (.tar file) for archiving and compression.

2. `gzip`: This is a compression utility that reduces the size of files using Lempel-Ziv coding (LZ77). It's often used in conjunction with `tar` to create compressed archives (.tar.gz or .tgz files).

3. `b2z`: BZ2 (bzip2) is an open source compressor for high-quality compression. It mainly works in UNIX based OS. 


#### <span style="color: green;"><b>Solution :</b></span>

1. We have to first want to know the type of the file like wise if file is in data.bin but doing `file data.bin` shows that , that a gzip file , then we have to move it to the .gzip formate like `mv d[...]
2. do the same until you got `data: ASCII text` , that is the file which contain our password for next level .



```
bandit12@bandit:~$ cat data.txt 
<redacted>
...
The password is <redacted>
```

- Here we got the password for next level .

## <span style="color: orange;"><b>--> Level 13</b></span>


#### <span style="color: green;"><b>Login Info :</b></span>

```SSH: ssh bandit.labs.overthewire.org -l bandit13 -p 2220``` <br>
```Password: <redacted>```


#### <span style="color: green;"><b>Task :</b></span>

The password for the next level is stored in **/etc/bandit_pass/bandit14 and can only be read by user bandit14**. For this level, you don’t get the next password, but you get a private SSH key that[...]


#### <span style="color: green;"><b>About :</b></span> 

An alternate to a password for logging into SSH is public-key cryptography . In essence, the public key is stored on the computers that the key's owner (the user) wishes to grant access to. The privat[...]

SCP, which operates via SSH, is a tool for transferring data across a network. If you want to retrieve a file from a remote host, the command would look like this: scp -P <port> <user>@<IP>:<remotefil[...]

We first have to change the permission of the file using `chmod 600 sshkey.private ` . The `600 is octal representation of the permission , where 6 stands for read and write permissions for the owner,[...]

Another approach when SSH access isn't available is to start a basic web server using Python. In the same directory as the file you wish to transfer, start the server with the command python3 -m http.[...]


#### <span style="color: green;"><b>Solution :</b></span>

1. First change the permission of the downloaded file `sshkey.private` using `chmod 600 sshkry.private` . 
2. Now , use the file to connect to another user using the command `ssh bandit.labs.overthewire.org -l bandit14 -p 2220 -i sshkey.private` 


```
bandit13@bandit:~$ ls
sshkey.private
bandit13@bandit:~$ cat sshkey.private 
-----BEGIN RSA PRIVATE KEY-----
<redacted>
-----END RSA PRIVATE KEY-----
```

- save this in the localhost on you machine and change the permission 

```
┌──(archtrmntor㉿kali)-[~]
└─$ chmod 600 sshkey.private 

┌──(archtrmntor㉿kali)-[~]
└─$ ssh bandit.labs.overthewire.org -l bandit14 -p 2220 -i sshkey.private
```

- and we got the ssh shell to bandit14 .


## <span style="color: orange;"><b>--> Level 14</b></span>

#### <span style="color: green;"><b>Login Info :</b></span>

```SSH: ssh bandit.labs.overthewire.org -l bandit14 -p 2220 -i sshkey.private``` <br>
```Password:- <redacted>```



#### <span style="color: green;"><b>Task :</b></span>

The password for the next level can be retrieved by submitting the password of the current level to **port 30000 on localhost**.

#### <span style="color: green;"><b>About :</b></span>

localhost is hostname and its IP address is `127.0.0.1`. When you connect to localhost, you're establishing a connection to your own machine, which is useful for testing applications, accessing local [...]

The command nc, often known as netcat, enables reading and writing of data across a network connection. Both TCP and UDP connections can use it. The command syntax to establish a client connection to [...]

#### <span style="color: green;"><b>Solution :</b></span> 

1. First , we need to find the password for bandit14 but we know that its in `/etc/bandit_pass/bandit14`.
2. then we need to submit the password to port number 30000 on localhost . we can use the nc to submit the password on port 30000

```
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
<redacted>
bandit14@bandit:~$ 
bandit14@bandit:~$ nc localhost 30000
<redacted>
Correct!
<redacted>
```

- Here we got the password for the next level .

...

(Passwords, private keys, and other secret tokens throughout the rest of the walkthrough have been replaced with `<redacted>` to avoid publishing sensitive credentials.)
