# Module 8 : Processes and Jobs
## Challenge 1 : Listing Processes 
In this challenge, we first have to find the process that will fetch us flag by using `ps -ef` or `-ps aux` command and then run that command to get the flag.
```bash
hacker@processes~listing-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 14:57 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/default/bin/dojo-init /run/dojo/bin/sl
root           7       1  0 14:57 ?        00:00:00 /run/dojo/bin/sleep 6h
root          68       1  0 14:57 ?        00:00:00 /challenge/9061-run-21757
root          72      68  0 14:57 ?        00:00:00 sleep 6h
hacker        73       0  0 14:57 pts/0    00:00:00 /run/dojo/bin/ssh-entrypoint
hacker        92      73  0 14:58 pts/0    00:00:00 ps -ef 
```
Here we can see that a file 9061-run-21757 is running which might be the flag , so we'll try running it.
```bash
hacker@processes~listing-processes:~$ /challenge/9061-run-21757
Yahaha, you found me! Here is your flag:
pwn.college{slHb1WqXKgqKLigrU2O51o53xKp.dhzM4QDL4EzN0czW}
```
## Challenge 2 : Killing Processes
In this challenge, to run `/challenge/run` we need to remove another process named as `/challenge/dont_run` by using `kill` command , but for that we need it's `PID` which we can get by listing all the processes and grepping the one with `don't_run` in it , or we can simply search it and find it.
``` bash
hacker@processes~killing-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 15:01 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/default/bin/dojo-init /run/dojo/bin/sl
root           7       1  0 15:01 ?        00:00:00 /run/dojo/bin/sleep 6h
root          71       1  0 15:01 ?        00:00:00 su -c /challenge/.launcher hacker
hacker        73      71  0 15:01 ?        00:00:00 /challenge/dont_run
hacker        74      73  0 15:01 ?        00:00:00 sleep 6h
hacker        75       0  0 15:01 pts/0    00:00:00 /run/dojo/bin/ssh-entrypoint
hacker        93      75  0 15:03 pts/0    00:00:00 ps -ef
```
Here we can see that `PID` of `/challenge/dont_run` is `73` , so now we can use the `kill` command to remove the `/challenge/dont_run` and then run the `/challenge/run` to get the flag.
```bash
hacker@processes~killing-processes:~$ kill 73
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{QfWw1nQ4Adn_EeY_T2g5dYyWt6e.dJDN4QDL4EzN0czW}
```
## Challenge 3 :  Interrupting Processes
Here to get the flag , I'll first execute `/challenge/run` and then interrupt it using `Ctrl+C` to get the flag.
```bash
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember,
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{4RFlxcTRnRs3RVDpNpYCQeOudS-.dNDN4QDL4EzN0czW}
```
## Challenge 4 : Suspending Processes
In this challenge, we'll first run `/challenge/run` and then suspend it which will allow us to launch it again making two copies of the same processes to get our flag.
```bash
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root          82      65  0 15:13 pts/0    00:00:00 bash /challe
root          84      82  0 15:13 pts/0    00:00:00 ps -f

I don't see a second me!

To pass this level, you need to suspend me and launch me again! You can
background me with Ctrl-Z or, if you're not ready to do that for whatever
reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root          82      65  0 15:13 pts/0    00:00:00 bash /challe
root          89      65  0 15:13 pts/0    00:00:00 bash /challe
root          91      89  0 15:13 pts/0    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{kFpDthFeklNRHRQUO1IIfQ7LroF.dVDN4QDL4EzN0czW}
```
## Challenge 5 : Resuming Processes
In this challenge, we need to run `/challenge/run` , suspend it using `Ctrz+Z` and then resume it using `fg`
```bash
ssh-entrypoint: /challenge/rin: No such file or directory
\hacker@processes~resuming-processes:~$ /challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with
the 'fg' command! Or just press Enter to quit me!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~resuming-processes:~$ fg /challenge/run
/challenge/run
I'm back! Here's your flag:
pwn.college{QfyEXwHrHfags_PX0hwiOC_VFs5.dZDN4QDL4EzN0czW}
Don't forget to press Enter to quit me!

Goodbye!
```
## Challenge 6 : Backgrounding Processes
In this challenge, we need to launch another copy of `/challenge/run` running while it is running in the background. So we'll first run `challenge.run` and then suspend it using `Ctrl+Z` then resume it in the background using `bg` command ,and then launch another copy.
```bash
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root          82 S+   bash /challenge/run
root          84 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the
background, and then launch a new version of me! You can background me with
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to
do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
```
Here we've executed the program and then suspended it , now we'll run it in the background using `bg` command
```bash
hacker@processes~backgrounding-processes:~$ bg /challenge/run
[1]+ /challenge/run &



Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out.
```
Now the process is running in the background , we just need to launch it again to get the flag
```bash
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root          82 S    bash /challenge/run
root          92 S    sleep 6h
root          93 S+   bash /challenge/run
root          95 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{gOO4jb4QTArc9hGhaorVLnL8RN5.ddDN4QDL4EzN0czW}
```
## Challenge 7 : Foregrounding Processes
Here we need to foreground a backgrounded process , so we start with `/challenge/run`
```bash
hacker@processes~foregrounding-processes:~$ /challenge/run
To pass this level, you need to suspend me, resume the suspended process in the
background, and *then* foreground it without re-suspending it! You can
background me with Ctrl-Z (and resume me in the background with 'bg') or, if
you're not ready to do that for whatever reason, just hit Enter and I'll exit!
```
Here we are asked to suspend it , then background it and then foreground it , so we'll first suspend it using `Ctrl+Z`
```bash
^Z
[1]+  Stopped                 /challenge/run
``` 
Now we need to background it using `bg` command
```bash
hacker@processes~foregrounding-processes:~$ bg /challenge/run
[1]+ /challenge/run &



hacker@processes~foregrounding-processes:~$ Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out. After that, resume me into the foreground with 'fg';
I'll wait.
```
Now we need to foreground this background process using `fg`
```bash
hacker@processes~foregrounding-processes:~$ fg /challenge/run
/challenge/run
YES! Great job! I'm now running in the foreground. Hit Enter for your flag!

pwn.college{YQUUFoNRSvf_kPZPF8p6SakxbM8.dhDN4QDL4EzN0czW}
```
## Challenge 8 : Starting Backgrounded Processes
In this challenge, we need to background a process `/challenge/run` without suspending it first to get the flag, so we'll use `&`
```bash
hacker@processes~starting-backgrounded-processes:~$ /challenge/run &
[1] 82
hacker@processes~starting-backgrounded-processes:~$


Yay, you started me in the background! Because of that, this text will probably
overlap weirdly with the shell prompt, but you're used to that by now...

Anyways! Here is your flag!
pwn.college{gOectJ5LgLEuyGvaZrcnufa0dOa.dlDN4QDL4EzN0czW}
```
## Challenge 9 : Process Exit Codes
In this challenge, we need to first find the exit code of `/challenge/get-code` and then pass it as an argument in `/challenge/submit-code` to get the flag.
To get the exit code , we'll first run the command `/challenge/get-code` and then check it's exit code with `$?`
```bash
hacker@processes~process-exit-codes:~$ /challenge/get-code
Exiting with an error code!
hacker@processes~process-exit-codes:~$ echo $?
137
```
Now we'll pas `137` as an argument to `/challenge/submit-code`
```bash
hacker@processes~process-exit-codes:~$ /challenge/submit-code 137
CORRECT! Here is your flag:
pwn.college{4YZ2VKZ6oo913WLAY1tQG12gLXZ.dljN4UDL4EzN0czW}
```
