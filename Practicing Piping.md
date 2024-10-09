# Module 6 : Practicing Piping
In this module we learn about how every  process in Linux have 3 channels of communications

A ***File Descriptor (FD)*** is a number the describes a communication channel in Linux 

 - Standard Input ***(stdin)*** `FD(0)`
 -  Standard Output ***(stdout)*** `FD(1)`
 - Standard Error ***(stderr)*** `FD(2)`

We learn about input & output redirection
### `>` is used to redirect *stdout* of commands to a file passed as an argument
### `>>` is used to append the *stdout* of a command to an existing file
### `2>` is used to redirect *stderr* of commands to a file
### `<` is used to redirect output of a file to *stdin* of a command
### `|` is used to redirect *stdout* of command to the left to *stdin* of a command to the right without needing to store results to a file.
### `>&` is used to redirect a file descriptor to another file descriptor (redirect fd on the left to fd on the right)
### `tee` duplicates the data flowing through pipes to any number of files provided as argument

### **Process substitution** (using `>(command)`) allows you to redirect the output of a command into the input of another command by treating the latter as a file.

## Challenge 1 : Redirecting output
Here we need to redirect the word `PWN` to a file `COLLEGE` , we can do this by redirecting the `stdout` of `echo PWN` to a file named `COLLEGE`. This can be done using `1>` OR just `>`
```bash
hacker@piping~redirecting-output:~$ echo PWN 1> COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your
flag:
pwn.college{cYiR1Zglkn40GEmFSygIMh3TQzl.dRjN1QDL4EzN0czW}
```
## Challenge 2 : Redirecting more output
In this challenge we need to redirect the `stdout` of a command `/challenge/run` to a file `myflag` , this can be done using `1>` or `>`
```bash
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
```
The `stdout` of `/chjallenge/run` get redirected to the file `myflag` and `stderr` gets printed on the terminal , to get the flag we can just read the contents of `myflag`
```bash
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{IKehNcNbTHdhLB4CryPEDeBEGKt.dVjN1QDL4EzN0czW}
```
## Challenge 3 : Appending output
Here we'll redirect the `stdout` of the command `/challenge/run` in append mode to a file `~/the-flag` and then we'll read the contents of `myflag` to get the flag
```bash
hacker@piping~redirecting-more-output:~$ /challenge/run >> ~/myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.

hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{IKehNcNbTHdhLB4CryPEDeBEGKt.dVjN1QDL4EzN0czW}
``` 
## Challenge 4 : Redirecting errors
In this challenge we'll redirecting the `stdout` of `/challenge/run` to `myflag` and `stderr` of `/challenge/run` to `instructions`
```bash
hacker@piping~redirecting-errors:~$  /challenge/run 2> instructions > myflag
hacker@piping~redirecting-errors:~$
```
We can see nothing gets printed to the terminal because we've redirected even the `stderr` to a file , to get the flag we'll read the contents of `myflag`
```bash
hacker@piping~redirecting-errors:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{kecXBBN0Q0nmo3RK_8D6uamkpoO.ddjN1QDL4EzN0czW}
```
## Challenge 5 : Redirecting input
In this challenge, we need to redirect the `stdin` of a file `PWN` containing `COLLEGE` to `stdin` of `/challenge/run`. So first we'll redirect `stdout` of `echo COLLEGE` to `PWN`, and then we'll redirect `PWN` to `stdin` of  `/challenge/run`
```bash
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{Qpn1akc9kZRzpCV397XmOHhwQtp.dBzN1QDL4EzN0czW}
```
## Challenge 6 : Grepping stored results
In this challenge, we'll first redirect the `stdout` of `/challenge/run` to `/tmp/data.txt` and then grep the line containing `pwn.college` from `/tmp/data.txt`
```bash
hacker@piping~grepping-stored-results:~$ grep pwn.college /challenge/run > /tmp/data.txt
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /tmp/data.txt
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to a file called /tmp/data.txt. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~grepping-stored-results:~$ grep pwn.college /tmp/d
ata.txt
pwn.college{AKFwcwbbWUIYwwDIICuGuNfuUZ3.dhTM4QDL4EzN0czW}
```
## Challenge 7 : Grepping live output
Here we'll redirect the `stdout` of `/challenge/run` to `stdin` of `grep pwn.college` using `|` operator.
```bash
hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{I3PzgLwjYkfbqpHZ-yR9KI0QaKw.dlTM4QDL4EzN0czW}
```
Here we can see that `stdout` of `/challenge/run` gets redirected to `stdin` of `grep pwn.college` and `stderr` of `/challenge/run` gets printed on the terminal, then the `stdout` of `grep pwn.college` gets printed on the terminal which contains the flag.
## Challenge 8 : Grepping errors
In this challenge we need to `grep pwn.college` on the `stderr` of  `/challenge/run` , but we know that `|` operator only redirect the `stdout` of a command , so we'll use `>&` operator to redirect the `stderr` of `/challenge/run` to `stdout` of `/challenge/run` and then pipe it using `|`.
```bash
hacker@piping~grepping-errors:~$ /challenge/run 2>&1 | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{oTdQe13N9CCuSV_y20V4hiu0EKm.dVDM5QDL4EzN0czW}
```
## Challenge 9 : Duplicating piped data with tee
In this challenge, we need to pipe the `stdout` of `/challenge/pwn` to `stdin` of `/challenge/college`.
```bash
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | /challenge/college
Processing...
The input to 'college' does not contain the correct secret code! This code
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the
output of 'pwn' and figure out what the code needs to be.
```
Here we can see something is missing from `/challenge/pwn` for `/challenge/college` to give the flag , so we'll see that by redirecting the `stdout` flow of `/challenge/pwn` using `tee`.
```bash
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee intercepting | /challenge/college
Processing...
The input to 'college' does not contain the correct secret code! This code
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the
output of 'pwn' and figure out what the code needs to be.
```
Here `tee` duplicated `stdout` of `/challenge/pwn` in a file named `intercepting` and we can see the `stderr` of `/challenge/college` printed on terminal because of some missing secret code. Now we print the contents of `intercepting`
```bash
hacker@piping~duplicating-piped-data-with-tee:~$ cat intercepting
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "scJgLkTR"
```
Here we can see that we should use `/challenge/pwn --secret` with argument `scJgLkTR` and then pipe it to `stdin` of  `/challenge/college`  to get the flag.
```bash
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --sec
ret scJgLkTR | /challenge/college
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{scJgLkTRKMpyFTEPjCnZxeG7HHP.dFjM5QDL4EzN0czW}
```
## Challenge 10 : Writing to multiple programs
In this challenge, we need to duplicate the `stdout` of `/challenge/hack` to `stdin` of two commands but `|` can only send `stdout` to `stdin` of one command , so here we can use `tee` to duplicate the `stdout` of `/challenge/hacker` and send it to a named pipe `>(/challenge/the)` and pipe the stdout of `tee` to `stdin` of `/challenge/planet` using `|`.
```bash
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/the) | /challenge/planet
Congratulations, you have duplicated data into the input of two programs! Here
is your flag:
pwn.college{kYRYaGZ6f0bcwpsOY8wwSTmPXOm.dBDO0UDL4EzN0czW}
```
**OR** we can duplicate the `stdout` of `/challenge/hacker` to two process substitutions simultaneously.
```bash
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/the) >(/challenge/planet)
This secret data must directly and simultaneously make it to /challenge/the and
/challenge/planet. Don't try to copy-paste it; it changes too fast.
305515291125817846
Congratulations, you have duplicated data into the input of two programs! Here
is your flag:
pwn.college{kYRYaGZ6f0bcwpsOY8wwSTmPXOm.dBDO0UDL4EzN0czW}
```
Here the `stdout` of `/challenge/hacker` is duplicated to process substitutions `/challenge/planet` and `/challenge/the` and then the `stdout` is also printed to the terminal which we can see as `This secret data must directly and simultaneously make it to /challenge/the and
/challenge/planet. Don't try to copy-paste it; it changes too fast.
305515291125817846`.
## Challenge 11 : Split-piping stderr and stdout
In this challenge we need to redirect the `stderr` of `/challenge/hack` to `/challenge/the` and `stdout` of `/challenge/hack` to `/challenge/planet` , we can do this by first redirecting the `stderr` of `/challenge/hack` to a process substitution `/challenge/the` and then pipe the `stdout` to `/challenge/planet`
```bash
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack 2> >(/challenge/the) | /challenge/planet
Congratulations, you have learned a redirection technique that even experts
struggle with! Here is your flag:
pwn.college{E2QbJO9TkRtZRhC8abXKwRH7iuB.dFDNwYDL4EzN0czW}
```
 
