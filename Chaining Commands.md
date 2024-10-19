# Module 11 : Chaining Commands

## Challenge 1 : Chaining with Semicolons
In this challenge, we need to chain two commands `/challenge/pwn` and `/challenge/college` using a `;`
```bash
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn;/challenge/college
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{cR9ele-4xIg2cQ-vqmZ3oyIn6Eh.dVTN4QDL4EzN0czW}
```
## Challenge 2 : Your First Shell Script
Here we need to create a bash file , by redirecting the output of `echo "/challenge/pwn;/challenge/college"` to `x.sh` and then running it using `bash`
```bash
hacker@chaining~your-first-shell-script:~$ echo "/challenge/pwn;/challenge/college" > x.sh
hacker@chaining~your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is the flag:
pwn.college{MLY-smctAapYJKjq6E2hINyhPkl.dFzN4QDL4EzN0czW}
```
## Challenge 3 : Redirecting Script Output 
To redirect output of multiple files into a `stdin` of single command , we can create a script file with the two commands and then redirect the output of the file using a `|` operator to `/challenge/solve`
```bash
hacker@chaining~redirecting-script-output:~$ echo "/challenge/pwn;/challenge/college" > x.sh
hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{MnBEEfX58s005GJByb-jKd3mx7J.dhTM5QDL4EzN0czW}
```

## Challenge 4 : Redirecting Executable Shell Scripts
In this challenge, we need to create a bash file which invokes `/challenge/solve` without using `bash` , so for that we'll make the script file executable and directly invoke it.
```bash
hacker@chaining~executable-shell-scripts:~$ echo /challenge/solve > x.sh
hacker@chaining~executable-shell-scripts:~$ chmod u+x x.sh
hacker@chaining~executable-shell-scripts:~$ ./x.sh
Congratulations on your shell script execution! Your flag:
pwn.college{0MWSMOpSyJ1m9lZT3HnPPR__eIv.dRzNyUDL4EzN0czW}
```
