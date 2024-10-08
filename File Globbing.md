# Module 5 : File Globbing
In this module we learn Globbing which is a process to match filenames or paths in shell. 
## Challenge 1 : Matching with *
In this we challenge, we need to `cd` to `/challenge` using only 4 or less characters as argument to `cd` , if we list the contents in `/` ,
```bash
hacker@globbing~matching-with-:~$ ls /
This challenge resets your working directory to /home/hacker unless you change
directory properly...
bin   challenge  etc   home  lib32  libx32  mnt  opt   root  sbin  sys  usr
boot  dev        flag  lib   lib64  media   nix  proc  run   srv   tmp  var
This challenge resets your working directory to /home/hacker unless you change
directory properly...
```
Here we can see only one directory starts with **c** , so we can say that `cd /c*` will `cd` to `/challenge` because only one directory matches the pattern.
```bash
hacker@globbing~matching-with-:~$ cd /c*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{Ui1U__UYBkzOw2yZUulAZcMAHFT.dFjM4QDL4EzN0czW}
```
## Challenge 2 : Matching with ?
`?` works for only one character , so to `cd` to `/challenge` without using `c` and `l` can be done by
```bash
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{IhDsLs3uIcoCl8-K8_8ZxxSIqq4.dJjM4QDL4EzN0czW}
```
## Challenge 3 : Matching with []
`[]` is a limited form of `?` in a way it will not try to match every character but only a selected few written inside it.
In the challenge we first have to `cd` to `/challenge/files` then we have to use a command `/challenge/run` and pass a single argument which globs 4 files which can be done using `[]`
```bash
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[b,a,s,h]
You got it! Here is your flag!
pwn.college{cHTfQPZZd1zYA-fKOrbXGFGZBzc.dNjM4QDL4EzN0czW}
```

## Challenge 4 : Matching paths with []
This is similar to the previous college , but here instead of **cd**ing to the `/challenge/files` directory , we'll pass the absolute paths of the files as argument to `/challenge/run`
```bash
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[b,a,s,h]
You got it! Here is your flag!
pwn.college{QYQtgL3STYCf-0i5d1JglXaCqxI.dRjM4QDL4EzN0czW}
```

## Challenge 5 : Mixing globs
As asked we need to `cd` to `/challenge/files` and see it's content and then pass a glob that will match only the given three files.
```bash
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ ls
amazing      delightful   great       jovial    magical     pwning   splendid   victorious  youthful
beautiful    educational  happy       kind      nice        queenly  thrilling  wonderful   zesty
challenging  fantastic    incredible  laughing  optimistic  radiant  uplifting  xenial
```
Here we can see there are 26 files and each files has a different first character (a-z) , so to glob `challenging` , `educational` & `pwning` , we'll use a glob `[cep]`
```bash
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{Isbx-eCzNtOWtK6wa-1RUUECnDY.dVjM4QDL4EzN0czW}
```
## Challenge 6 : Exclusionary globbing
This is similar to the previous problem, first we `cd` to `/challenge/files` and then glob all the files that don't start with **p w n** by globbing `[^pwn]`
```bash
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [^pwn]*
You got it! Here is your flag!
pwn.college{IrgBdMf6GnkPfkoYF_ouZLz_lOz.dZjM4QDL4EzN0czW}
```
