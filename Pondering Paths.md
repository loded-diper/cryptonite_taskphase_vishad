# Module 2 : Pondering Paths
This module teaches the basics of Linux file paths. The Linux filesystem is structured like a tree, starting from the root directory (`/`). Each file or directory is accessed by following a path from the root, with each level separated by `/`.

## Challenge 1 : The Root
In this we invoke a program set up in the root directory named as `pwn` , we start in `~` so to invoke `pwn` we do it by it's absolute path which is `/pwn`
```bash
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{gavTJwuLO2iwYptgM50OcCGD6sA.dhzN5QDL4EzN0czW}
```
## Challenge 2 : Program and absolute paths
In this we invoke a program `run` which is inside a `challenge` & this `challenge` directory is in the `/` root directory. Starting in the `~` directory, we can invoke `run` by it's absolute path which is `/challenge/run`
```bash 
hacker@paths~program-and-absolute-paths:~$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{YRno2Aeo1tzrDw1JFrwFJXNyw9i.dVDN1QDL4EzN0czW} 
```
## Challenge 3 : Position thy self
### `cd` command
***Here we learn about this new command which is used to navigate to any directory by passing it's absolute path as a argument.***
We have to invoke the program `run` but from a certain directory which is not given , so we try to invoke it from `~`.
```bash
hacker@paths~position-thy-self:~$ /challenge/run
Incorrect...
You are not currently in the /proc/67 directory.
```
After invoking `run` from `~` , we got error which stated that we are not in the `/proc/67` directory. So we'll have to navigate to that directory and invoke `run` from there.
```bash
hacker@paths~position-thy-self:~$ cd /proc/67
hacker@paths~position-thy-self:/proc/67$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{gB2HAT2D-7Vx4ttAU3RfkgGWlTV.dZDN1QDL4EzN0czW}
```
## Challenge 4 : Position elsewhere
This challenge is similar to the previous one , first we try to invoke `run` from `~` , then we get the directory which we need to invoke it from , hence we navigate to that directory and invoke it from there.
```bash
hacker@paths~position-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /sys directory.

hacker@paths~position-elsewhere:~$ cd /sys
hacker@paths~position-elsewhere:/sys$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{8PCmKN7MjBDbw2PZVptnu7EBl-J.ddDN1QDL4EzN0czW}
```
## Challenge 5 : Position yet elsewhere
This challenge is yet again similar to the previous ones, where we need to invoke `run` from any directory , then we get the required directory to invoke it from which we navigate to and then invoke `run`
```bash
hacker@paths~position-yet-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /etc/apt/sources.list.d directory.

hacker@paths~position-yet-elsewhere:~$ cd /etc/apt/sources.list.d
hacker@paths~position-yet-elsewhere:/etc/apt/sources.list.d$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{sovjj8gH16c4Lnut3WLKSXcs0Ao.dhDN1QDL4EzN0czW} 
```
## Challenge 6 : Implicit relative paths, from /
*In this challenge we learn about relative paths, that how we don't need to give absolute path to invoke a program if we are in the directory/parent directory , to where it is located.*

Here we have to invoke `run` using relative path which start with c *(which might be referring to the challenge directory)*. The relative path required to execute `run` is `challenge/run`, but for this to work as expected we need to be in the parent directory of `challenge` which is the root directory `/`. 
So first we change the directory to `/` from `~` then we invoke `run` using it's relative path.
```bash
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{IBxyc5uQnaqX_7rbDicZUYAvI3h.dlDN1QDL4EzN0czW}
```
## Challenge 7 : explicit relative paths, from /
*In this challenge we learn about a special entry `.` which refers to the current directory. This used from the root directory `/` is same as the absolute path.*
In this we need to invoke `run` using relative path , so we follow the same approach as previous challenge which is `cd` to `/` and then invoke `run` by relative path `challenge/run`.
```bash
hacker@paths~explicit-relative-paths-from-:~$ cd /
hacker@paths~explicit-relative-paths-from-:/$ challenge/run
Incorrect...
This challenge must be called with a relative path that explicitly starts with a `.`!
```
But this challenge requires us to use a relative path that start from `.` , so we use `./challenge/run` which is a relative path (in general).
```bash
hacker@paths~explicit-relative-paths-from-:/$ ./challenge/run
Correct!!!
./challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{8HIKOzUfBsNXJnSWn1w4Zb7nVXa.dBTN1QDL4EzN0czW}
```
## Challenge 8 : implicit relative path
*Here we learn the use of `.` , if we need to invoke a program in cwd , we can't invoke it by just writing it's name `run` (assuming program name is "run"). This is a safety measure of linux to prevent accidentally running programs that might share the same name as other system commands.*

In this challenge we need to invoke `run` from `challenge` directory , so as we know we can't invoke it by `run` , we'll have to tell linux  to explicitly run a program in cws using `.`
```bash
hacker@paths~implicit-relative-path:~$ cd /challenge
hacker@paths~implicit-relative-path:/challenge$ ./run
Correct!!!
./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{cb_ucISYIQCgW8lhz1sxpo_8xuv.dFTN1QDL4EzN0czW}
```

### `~` directory 
We learn that this `~` is a shorthand for /home/`username`. The expansion of `~` is absolute path.
Also note that only the expansion of the leading ~ will be considered as absolute path, rest will be considered as other file/directory.

## Challenge 9 : home sweet home
In this challenge we are given a command `/challenge/run` which will write a copy of out flag to any path we pass as an argument with the following constraints.
 1.  Your argument must be an absolute path.
 2.  The path must be inside your home directory.
 3.  Before expansion, your argument must be three characters or less.
 
 expansion of `~` will be absolute path and inside the `home` directory , now for the last constraint (that the arguments must be 3 characters or less) , we need to have the filename of a single character to keep the argument of 3 characters.
So our argument should be ~/`any character`
```bash
hacker@paths~home-sweet-home:~$ /challenge/run ~/a
Writing the file to /home/hacker/a!
... and reading it back to you:
pwn.college{ovVzludK8rOnYkIR7n_LrPbOkM5.dNzM4QDL4EzN0czW}
```
