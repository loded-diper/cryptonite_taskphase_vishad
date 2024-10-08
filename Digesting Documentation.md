# Module 4 : Digesting Documentation
In this module we learn how to read documentation of commands and apply them in various programs.
### `man` command
This command is short for **manual** and displays the manual of the command passed as an argument. These manuals are stored in a centralized database in `/usr/share/man`
### `help` argument
Some commands don't have a manual page , instruction on these commands can be invoked with this `-- help`OR `-h` OR`-?` OR `help` argument.

## Challenge 1 :  Learning from Documentation
In this challenge , we are given the documentation of a command `/challenge/challenge` which requires a argument `--giveflag` to be passed along with it for the command to run properly.
```bash
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{k9GHviq7e8VtGKJBKSp8kWthQQ6.dRjM5QDL4EzN0czW}
```
## Challenge 2 : Learning Complex Usage
In this challenge we are required to print the `flag` which is in `/` directory using aa command `/challenge/challenge` and it's argument `--printfile`.
```bash
hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile /flag
Correct argument! Here is the /flag file:
pwn.college{oilsTNeNi3wZnQoG3fVHhiY97nS.dVjM5QDL4EzN0czW}
```
## Challenge 3 : Reading Manuals
In this challenge, we need to find the secret option in manpage of `challenge` to print the flag.
```bash
CHALLENGE(1)          Challenge Commands          CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --uplynr NUM
              print the flag if NUM is 793

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The  repository for this dojo: <https://github.com/pwn‐
       college/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)

pwn.college                May 2024               CHALLENGE(1)
```
We can see we need to use this command as `/challenge/challenge` and pass argument `--uplynr` with NUM = `793` to print the flag.
```bash
hacker@man~reading-manuals:~$ /challenge/challenge --uplynr 793
Correct usage! Your flag: pwn.college{UUJDB7K9uJ3pJl4ynP5BryaBexE.dRTM4QDL4EzN0czW}
```
## Challenge 4 : Searching Manuals
Upon searching through the manual of `challenge` we learn that the correct usage is `/command/command` and the argument to be passed to print flag is `--wg` after pressing `/` and searching for `flag` in the man page.
```bash
hacker@man~searching-manuals:~$ /challenge/challenge --wg
Initializing...
Correct usage! Your flag: pwn.college{I0MwMGpMDVHpsxqNJEQoUit6eWm.dVTM4QDL4EzN0czW}
```
## Challenge 5 : Searching For Manuals
In this we don't know the manpage to look for to use `/challenge/challenge` properly, so we'll first see the manpage of `man`  ny using `man man`
```bash
man -k printf
Search the short descriptions and manual page names for the keyword printf  as  regular  expression.   Print  out  any
matches.  Equivalent to apropos printf.
```
Upon browsing through some arguments , we see this argument `-k` which searches the string passed to it as argument in the description.
So we can search for `flag` in the description OR we can also search `/challenge/challenge` because we are told in the question that the description will contain this no matter the name of the command.
```bash
hacker@man~searching-for-manuals:~$ man -k /challenge/challenge
wlvvysmkxj (1)       - print the flag!
``` 
So now we know the command which is used for printing the flag , so now we can access the manual for this command.
```bash
hacker@man~searching-for-manuals:~$ man wlvvysmkxj

CHALLENGE(1)                                            Challenge Commands                                           CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --wlvvys NUM
              print the flag if NUM is 024

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The repository for this dojo: <https://github.com/pwncollege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)

pwn.college                                                  May 2024                                                CHALLENGE(1)
```
Here we can see to print the flag, the name of the command used is `/challenge/challenge` and the argument passed along with it is `--wlvvys` with the correct NUM which is `024`
```bash
hacker@man~searching-for-manuals:~$ /challenge/challenge --wlvvys 024
Correct usage! Your flag: pwn.college{w0OKlRvJvysmGLkxGjBRRqEU2zT.dZTM4QDL4EzN0czW}
```

## Challenge 6 : Helpful Programs
In this challenge, we'll have to learn from the instruction given by `--help` argument to `/challenge/challenge` command. 
```bash
hacker@man~helpful-programs:~$ challenge --help
ssh-entrypoint: challenge: command not found
hacker@man~helpful-programs:~$ /challenge/challenge --help
usage: a challenge to make you ask for help [-h] [--fortune]
                                            [-v]
                                            [-g GIVE_THE_FLAG]
                                            [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct
                        value
  -p, --print-value     print the value that will cause the -g
                        option to give you the flag
```
So we can see to get the flag we need to pass the argument `-g` with another argument `GIVE_THE_FLAG` and the flag will only be printed when the value of this argument is correct which we will get through another argument `-p`.
```bash
hacker@man~helpful-programs:~$ /challenge/challenge -p
The secret value is: 14
hacker@man~helpful-programs:~$ /challenge/challenge -g 14
Correct usage! Your flag: pwn.college{sHk0R_XCVhwNEUaii1tdaFeXHoj.ddjM4QDL4EzN0czW}
```

## Challenge 7 : Help for Builtins
In this challenge , `challenge` is a builtin , so we'll get it's information using `help`
```bash
hacker@man~help-for-builtins:~$ help challenge
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!

    Options:
      --fortune         display a fortune
      --version         display the version
      --secret VALUE    prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "EtO9jtbh".
```
To print the flag we need to pass the argument `secret` along with the value `EtO9jtbh`.
```bash
hacker@man~help-for-builtins:~$ challenge --secret EtO9jtbh
Correct! Here is your flag!
pwn.college{EtO9jtbh4-MEs1LOsYZ_8vPEvFb.dRTM5QDL4EzN0czW}
``` 