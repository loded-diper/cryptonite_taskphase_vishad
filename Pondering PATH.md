# Module 12 : Pondering PATH

## Challenge 1 : The PATH Variable 
The challenge here was to stop the `/challenge/run` program from finding the `rm` command so that it couldn’t delete the flag. First, I cleared the `PATH` environment variable, Then, I ran the `/challenge/run` program
```bash
hacker@path~the-path-variable:~$ PATH=""
hacker@path~the-path-variable:~$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{Q-BsAfLK1-800IDG0r-ccNUdoZn.dZzNwUDL4EzN0czW}
```
## Challenge 2 : Setting PATH
I had to alter the `PATH` to make the `/challenge/run` program able to find the `win` command. The `win` command had to be accessible using just its name. I pointed the `PATH` variable to the directory where `win` was located, Then, I ran the `/challenge/run` program:
```bash
hacker@path~setting-path:~$ PATH="/challenge/more_commands/"
hacker@path~setting-path:~$ /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{EiVxVINTW9eVXVklXJE78_RSOHK.dVzNyUDL4EzN0czW}
```
## Challenge 3 : Adding Commands
The goal was to create a shell script named `win` that reads the flag file, and modify the `PATH` so `/challenge/run` could find it. I made a simple `win` script to read the flag and then after that i made it executable. Then checked the current `PATH` to know address of `cat` , I updated the `PATH` to include the directories where `win` script was. Then executed `/challenge/run`
```bash
hacker@path~adding-commands:~$ touch win
hacker@path~adding-commands:~$ echo cat /flag > win
hacker@path~adding-commands:~$ chmod u+x win
hacker@path~adding-commands:~$ echo $PATH
/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
hacker@path~adding-commands:~$ PATH="/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/hacker"
hacker@path~adding-commands:~$ /challenge/run
Invoking 'win'....
pwn.college{sCRzSm3M5cmvWBEKlkLrL-ZUGtg.dZzNyUDL4EzN0czW}
```
## Challenge 4 : Hijacking Commands
I needed to stop the flag from being deleted by hijacking the `rm` command with a custom script that reads the flag instead. I wrote a shell script named `rm` to replace the `rm` functionality with `cat` to read the flag. Then, I made it executable , I updated the `PATH` so that `/challenge/run` would use my custom `rm` script , Finally, I ran `/challenge/run`.
```bash
hacker@path~hijacking-commands:~$ find / -name cat
find: ‘/root’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
find: ‘/tmp/tmp.G9qthVCks5’: Permission denied
/usr/bin/cat
/usr/share/doc/zsh-common/examples/Functions/cat
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/cache/private’: Permission denied
find: ‘/var/log/private’: Permission denied
find: ‘/var/log/apache2’: Permission denied
find: ‘/var/log/mysql’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/mysql-keyring’: Permission denied
find: ‘/var/lib/php/sessions’: Permission denied
find: ‘/var/lib/private’: Permission denied
find: ‘/var/lib/mysql-files’: Permission denied
find: ‘/var/lib/mysql’: Permission denied
/run/workspace/bin/cat
find: ‘/run/mysqld’: Permission denied
find: ‘/run/sudo’: Permission denied
find: ‘/proc/tty/driver’: Permission denied
find: ‘/proc/1/task/1/fd’: Permission denied
find: ‘/proc/1/task/1/fdinfo’: Permission denied
find: ‘/proc/1/task/1/ns’: Permission denied
find: ‘/proc/1/fd’: Permission denied
find: ‘/proc/1/map_files’: Permission denied
find: ‘/proc/1/fdinfo’: Permission denied
find: ‘/proc/1/ns’: Permission denied
find: ‘/proc/7/task/7/fd’: Permission denied
find: ‘/proc/7/task/7/fdinfo’: Permission denied
find: ‘/proc/7/task/7/ns’: Permission denied
find: ‘/proc/7/fd’: Permission denied
find: ‘/proc/7/map_files’: Permission denied
find: ‘/proc/7/fdinfo’: Permission denied
find: ‘/proc/7/ns’: Permission denied
/opt/busybox/busybox-1.33.2/testsuite/cat
/opt/busybox/busybox-1.33.2/_install/bin/cat
/opt/aflplusplus/nyx_mode/packer/linux_initramfs/rootTemplate/bin/cat
/nix/store/k71apxkm38m3g34k01sb6zhysi0y7gph-coreutils-9.5/bin/cat
/nix/store/hgcmc7ps7wr0sxnbc87g4ba970km2vy4-dojo-workspace-full/bin/cat
/nix/store/a18ji16bi5ws1zksk1jwrx8dir6rdbhi-dojo-workspace-full/bin/cat
/nix/store/h8k7v1w69b9fs60jkx59vkhpy6scwgap-dojo-workspace-full/bin/cat
/nix/store/vapa6rnwfvbm3srldx33nyy2ybz9iqpy-dojo-workspace-full/bin/cat
/nix/store/6sin45s97yp4cfdn3q74drsjd7f4cq1f-dojo-workspace-full/bin/cat
/nix/store/nlxcqrgiszbjqkq86qhnflrbrs4adaac-dojo-workspace-full/bin/cat
/nix/store/cakzg9vppcbxwq046nlbi6xmib3xx4ka-dojo-workspace-full/bin/cat
/nix/store/mjnsl8dps0vn3aaf9wpgk4n830x320a7-dojo-workspace-full/bin/cat
/nix/store/nsh8bjqlami5grymm2mv63plmncga7wk-dojo-workspace-full/bin/cat
hacker@path~hijacking-commands:~$ touch rm
hacker@path~hijacking-commands:~$ echo /usr/bin/cat /flag > rm
hacker@path~hijacking-commands:~$ chmod u+x rm
hacker@path~hijacking-commands:~$ PATH="/home/hacker"
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
pwn.college{kXfn_ZqPlVP0JFVsKKEtTUio187.ddzNyUDL4EzN0czW}
```