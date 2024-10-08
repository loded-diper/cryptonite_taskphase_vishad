# Module 3 : Comprehending Commands
In this module we learn many new commands
### `cat` command
This command is read out a file or if passed with multiple arguments/files , it will con**cat**nate all of them and read them out.
### `grep` command
This command is used to search for a specific line containing a `string` passed as an argument from the while text file.
### `ls` command
This command lists all the files in the directories provided to it as arguments. But some files whose name starts with `.` are hidden and not listed using `ls` , to list all the files including the hidden files in a directory we pass a extra argument `-a` with `ls`. 
### `touch` command
This command is used to create a new blank file in the cwd
### `rm` command
This command is used to delete all the files passed to it as arguments.
### `mkdir` command
This command is used to create a new directory in the cwd 
### `find` command
This command is used to find files/directories in the given parent directory , if not given, it searches in cwd.
### `ln` command
This command is used to create references to a file/directory so that the file can be accessed by multiple application at once.
These are of two types (i) hard link (ii) soft link (symlink)
### `find` command 
This command is used to find the type of file which is passed as argument. Eg- ASCII , Symbolic link..

## Challenge 1 : cat : not the pet, but the command!
In this command we need to read the data of the file `flag` which can be accomplished by using the command `cat` , we can use `cat ~/flag` to read the file as it is in the home directory , or we can just do `cat flag` because our cwd is `~` when we start the shell. 
```bash
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{ULb9LRPyE9ed7nx-k_A-QV5I_Dz.dFzN1QDL4EzN0czW}
```
## Challenge 2 :  catting absolute paths
In this challenge we need to read the file `flag` which is in the root directory `/` , so we can pass absolute path of the file as an argument to cat which will look like `cat /flag`.
```bash
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{8BKoanvCjECcU36ZFwMkf-bsXJW.dlTM5QDL4EzN0czW}
```
## Challenge 3 : more catting practice
In this challenge, we needed to cat the file `flag` without **cd**ing to the directory in which flag is present. Upon starting the challenge , we found the absolute path of flag , so we can directly pass the absolute path of the file `flag` as an argument in bash.
```bash
You cannot use the 'cd' command in this level, and must retrieve the flag by
absolute path. Plus, I hid the flag in a different directory! You can find it
in the file /usr/include/netash/flag. Go cat it out **without** cding into that
directory!
hacker@commands~more-catting-practice:~$ cat /usr/include/netash/flag
pwn.college{Y9MK1BeABLuM7oM13miPwlueko7.dBjM5QDL4EzN0czW}
```
## Challenge 4 : grepping for a needle in a haystack
In this challenge we have to find the flag from a file with large lines of text , so i'll need to grep the line in which the string `pwn.college` is present as the flag starts with `pwn.college`.
```bash
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{0WFNkUNjkfY7tvudB11q4vv_1zv.ddTM4QDL4EzN0czW}
```
## Challenge 5 : listing files
In this challenge , we need to execute the file `run` to get the flag , but the file has been renamed, so to start we'll list all the files in the `challenge` directory.
```bash
hacker@commands~listing-files:~$ ls /challenge
4651-renamed-run-29391  DESCRIPTION.md
```
There are 2 files in the `challenge` directory & we can see the `run` file is renamed to  `4651-renamed-run-29391` file , so we'll execute this file.
```bash
hacker@commands~listing-files:~$ /challenge/4651-renamed-run-29391
Yahaha, you found me! Here is your flag:
pwn.college{wBMBNRTL6bMuvyqgzGqI75S0qrX.dhjM4QDL4EzN0czW}
```
## Challenge 6 : touching files
In this challenge we need to create two files namely `pwn` and `college` in the `/tmp` directory. We can either `cd` to the `/tmp` directory and use `touch pwn college` there **OR** we can just give the absolute paths of the files as an argument.
```bash
hacker@commands~touching-files:~$ touch /tmp/pwn /tmp/college
hacker@commands~touching-files:~$ /challenge/run
Success! Here is your flag:
pwn.college{kLQjNnUAoWo8KZ4HLX-2WnQ3ILt.dBzM4QDL4EzN0czW}
```
## Challenge 7 : removing files
In this challenge, to get the flag we need to delete `delete_me` file in the `~` and then run `/challenge/check` , so we'll use the `rm` command to remove the file.
```bash
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{wZVXNtb8X6L-xWzRDFIBObnyNN2.dZTOwUDL4EzN0czW}
```
## Challenge 8 : hidden files
In this challenge , we need to find the `flag` file in `/` directory but it is hidden , so we'll have to pass `-a` argument along with `ls` after **cd**ing to the `/` directory to find the file **OR** we can directly pass the `/` directory as an argument in `ls`.
```bash
hacker@commands~hidden-files:/$ ls -a /
.                    bin        etc    lib64   nix   run   tmp
..                   boot       home   libx32  opt   sbin  usr
.dockerenv           challenge  lib    media   proc  srv   var
.flag-7829121118389  dev        lib32  mnt     root  sys
```
Here we can see the dot-prepended `flag` file is named as `.flag-7829121118389` , we'll just read this file to get the flag.
```bash
hacker@commands~hidden-files:~$ cat /.flag-7829121118389
pwn.college{UDmanto6rEC5y9O0OacVD2factK.dBTN4QDL4EzN0czW}
```
## Challenge 9 : An Epic Filesystem Quest
In this challenge , we need to find the files in `/` to get the first clue.
```bash
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls
CUE   challenge  flag  lib32   media  opt   run   sys  var
bin   dev        home  lib64   mnt    proc  sbin  tmp
boot  etc        lib   libx32  nix    root  srv   usr
```
We can see a file name `CUE` , we need to open it to proceed further
```bash
hacker@commands~an-epic-filesystem-quest:/$ cat CUE
Lucky listing!
The next clue is in: /opt/busybox/busybox-1.33.2/include/config/feature/top/smp

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
```
Here we are told that next cue is in `/opt/busybox/busybox-1.33.2/include/config/feature/top/smp` directory and we need to find it without **cd**ing to that directory. So we'll list the files present in that directory by giving the absolute path of the directory as an argument.
```bash
hacker@commands~an-epic-filesystem-quest:/$ ls /opt/busybox/busybox-1.33.2/include/config/feature/top/smp
MESSAGE-TRAPPED  cpu.h  process.h
```
We found the file for the next clue which is `MESSAGE-TRAPPED` , let's read it's content by giving it's absolute path as an argument to `cat`
```bash
hacker@commands~an-epic-filesystem-quest:/$ cat /opt/busybox/busybox-1.33.2/include/config/feature/top/smp/MESSAGE-TRAPPED
Great sleuthing!
The next clue is in: /usr/local/lib/python3.8/dist-packages/plumbum/commands

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
```
We'll repeat the process for `/usr/local/lib/python3.8/dist-packages/plumbum/commands` directory.
```bash
hacker@commands~an-epic-filesystem-quest:/$ ls /usr/local/lib/py
thon3.8/dist-packages/plumbum/commands
TEASER-TRAPPED  __pycache__  daemons.py    processes.py
__init__.py     base.py      modifiers.py
```
We'll read the contents of `TEASER-TRAPPED` file.
```bash
hacker@commands~an-epic-filesystem-quest:/$ cat /usr/local/lib/python3.8/dist-packages/plumbum/commands/TEASER-TRAPPED
Yahaha, you found me!
The next clue is in: /opt/linux/linux-5.4/include/config/x86/local

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
```
Here we are asked to `cd` to the `/opt/linux/linux-5.4/include/config/x86/local` directory and look for further clues there , which we'll do by listing the files in that directory.
```bash
hacker@commands~an-epic-filesystem-quest:/$ cd /opt/linux/linux-5.4/include/config/x86/local
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/include/config/x86/local$ ls
SNIPPET  apic.h
```
We need to read the contents of `SNIPPET` to get the next clue.
```bash
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/include/config/x86/local$ cat SNIPPET
Yahaha, you found me!
The next clue is in: /usr/local/lib/python3.8/dist-packages/jupyter_lsp/specs

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
```
Here we need to list the files in `/usr/local/lib/python3.8/dist-packages/jupyter_lsp/specs` directory and read the contents of the file in which next clue is present without **cd**ing to the directory.
```bash
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/include/config/x86/local$ ls /usr/local/lib/python3.8/dist-packages/jupyter_lsp/specs
NUGGET-TRAPPED
__init__.py
__pycache__
bash_language_server.py
config
dockerfile_language_server_nodejs.py
javascript_typescript_langserver.py
jedi_language_server.py
julia_language_server.py
pyls.py
pyright.py
python_lsp_server.py
r_languageserver.py
sql_language_server.py
texlab.py
typescript_language_server.py
unified_language_server.py
utils.py
vscode_css_languageserver.py
vscode_html_languageserver.py
vscode_json_languageserver.py
yaml_language_server.py
```
We'll read the contents of `NUGGET-TRAPPED` to get the next clue
```bash
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/include/config/x86/local$ cat /usr/local/lib/python3.8/dist-packag
es/jupyter_lsp/specs/NUGGET-TRAPPED
Yahaha, you found me!
The next clue is in: /etc/john

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
```
We'll repeat the same procedure for `/etc/john` directory.
```bash
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/include/config/x86/local$ ls /etc/john
SPOILER-TRAPPED  john-mail.conf  john-mail.msg  john.conf
```
We'll read the contents of `SPOILER-TRAPPED` to get the next clue
```bash
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/include/config/x86/local$ cat /etc/john/SPOILER-TRAPPED
Congratulations, you found the clue!
The next clue is in: /usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/Latin-Modern/Size2/Regular
```
No conditions have been put forth , so we'll cd to the `/usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/Latin-Modern/Size2/Regular` directory and list it's contents.
```bash
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/include/config/x86/local$ cd /usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/Latin-Modern/Size2/Regular
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/Latin-Modern/Size2/Regular$ ls
BLUEPRINT  Main.js
```
we'll read the contents of `BLUEPRINT` to proceed further.
```bash
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/Latin-Modern/Size2/Regular$
 cat BLUEPRINT
Yahaha, you found me!
The next clue is in: /usr/lib/jvm/java-11-openjdk-amd64/bin

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
```
As instructed, we'll first `cd` into the `/usr/lib/jvm/java-11-openjdk-amd64/bin` directory and list it's contents to get the file for next clue.
```bash
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/Latin-Modern/Size2/Regular$ cd /usr/lib/jvm/java-11-openjdk-amd64/bin
hacker@commands~an-epic-filesystem-quest:/usr/lib/jvm/java-11-openjdk-amd64/bin$ ls
POINTER  jjs      pack200  rmiregistry
java     keytool  rmid     unpack200
```
Now we'll read the contents of `POINTER` to get to the next clue.
```bash
hacker@commands~an-epic-filesystem-quest:/usr/lib/jvm/java-11-openjdk-amd64/bin$ cat POINTER
Great sleuthing!
The next clue is in: /usr/lib/debug/.build-id/6c

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
```
We'll list all the files, including the hidden ones by passing `-a` along with `ls` and `/usr/lib/debug/.build-id/6c`
```bash
hacker@commands~an-epic-filesystem-quest:/usr/lib/jvm/java-11-openjdk-amd64/bin$ ls -a /usr/lib/debug/.build-id/6c
.
..
.LEAD
0eda7cbd84ce0e5f4ad0f277d47a2fdc6101fe.debug
4ee201a50aec2e6af9ed410c404e717316ad6d.debug
b000012fb0283811d939cfe478f153e49a6eb8.debug
eacb2bf094547b38536ec42d56d320da03cd77.debug
```
We'll read the contents of `.LEAD`
```bash
hacker@commands~an-epic-filesystem-quest:/usr/lib/jvm/java-11-openjdk-amd64/bin$ cat /usr/lib/debug/.build-id/6c/.LEAD
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{gzSoh976ZJunJQx4A4KSTD_awv7.dljM4QDL4EzN0czW}
```
## Challenge 10 : making directories
In this challenge, we need to create a `pwn` directory in `/tmp` and create a `colleeg` file inside that directory to get the flag.
We can do this after **cd**ing to the `/tmp` and then making directories and file , or we can just pass absolute path of directory and file to `mkdir` and `touch`
```bash
hacker@commands~making-directories:~$ mkdir /tmp/pwn
hacker@commands~making-directories:~$ touch /tmp/pwn/college
hacker@commands~making-directories:~$ /challenge/run
Success! Here is your flag:
pwn.college{YRcTNGnolqwRhiNQMFhB0oHPQai.dFzM4QDL4EzN0czW}
```
## Challenge 11 : finding files
We need to find the file `flag` which can be kept anywhere  , so we'll pass 2 arguments with the command `find`, first will be the path of the parent directory which will be `/` in this case because the file can be kept anywhere, second argument will be the name of the file which is `flag`.
```bash
hacker@commands~finding-files:~$ find / -name flag
find: ‘/root’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
find: ‘/tmp/tmp.G9qthVCks5’: Permission denied
/usr/local/share/radare2/5.9.5/flag
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
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
/opt/linux/linux-5.4/sound/isa/es1688/flag
/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag
/opt/radare2/libr/flag
/nix/store/pmvk2bk4p550w182rjfm529kfqddnvh3-python3.11-pwntools-4.12.0/lib/python3.11/site-packages/pwnlib/flag
/nix/store/1yagn5s8sf7kcs2hkccgf8d0wxlrv5sz-radare2-5.9.0/share/radare2/5.9.0/flag
```
We can see many directories denied permission to access their content , which was expected , but we need to focus on the files which came through as results, which are 
`/usr/local/share/radare2/5.9.5/flag`
`/usr/local/lib/python3.8/dist-packages/pwnlib/flag`
`/opt/linux/linux-5.4/sound/isa/es1688/flag`
`/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag`
`/opt/radare2/libr/flag`
`/nix/store/pmvk2bk4p550w182rjfm529kfqddnvh3-python3.11-pwntools-4.12.0/lib/python3.11/site-packages/pwnlib/flag`
`/nix/store/1yagn5s8sf7kcs2hkccgf8d0wxlrv5sz-radare2-5.9.0/share/radare2/5.9.0/flag`
The flag we need is in one of these text files , so we can read the content of each file until we get our required flag **OR** we can grep the `pwn.college` by passing absolute path of each file to get the desired flag.
```bash
hacker@commands~finding-files:~$ grep pwn.college /usr/local/share/radare2/5.9.5/flag /usr/local/lib/python3.8/dist-packages/pwnlib/flag /opt/linux/linux-5.4/sound/isa/es1688/flag /opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag /opt/radare2/libr/flag nix/store/pmvk2bk4p550w182rjfm529kfqddnvh3-python3.11-pwntools-4.12.0/lib/python3.11/site-packages/pwnlib/flag /nix/store/1yagn5s8sf7kcs2hkccgf8d0wxlrv5sz-radare2-5.9.0/share/radare2/5.9.0/flag
grep: /usr/local/share/radare2/5.9.5/flag: Is a directory
grep: /usr/local/lib/python3.8/dist-packages/pwnlib/flag: Is a directory
/opt/linux/linux-5.4/sound/isa/es1688/flag:pwn.college{g49h56bMAB45FVPmbzo3bV_ysdR.dJzM4QDL4EzN0czW}
grep: /opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag: Is a directory
grep: /opt/radare2/libr/flag: Is a directory
grep: nix/store/pmvk2bk4p550w182rjfm529kfqddnvh3-python3.11-pwntools-4.12.0/lib/python3.11/site-packages/pwnlib/flag: Is a directory
grep: /nix/store/1yagn5s8sf7kcs2hkccgf8d0wxlrv5sz-radare2-5.9.0/share/radare2/5.9.0/flag: Is a directory
```
Here we can see all other paths were a directory , only `/opt/linux/linux-5.4/sound/isa/es1688/flag` is a file and had the the flag.
## Challenge 12 : linking files
In this level we need to create a symbolic link such that executing `/challenge/catflag` points to `/flag` , this can be done by creating a symbolic link between `~/not-the-flag` and `/flag`, as executing `/challenge/catflag` will read out `~/not-the-flag` which is symbolic link to `/flag` , so we get the flag.
```bash
hacker@commands~linking-files:~$ ln -s /flag ~/not-the-flag
hacker@commands~linking-files:~$ /challenge/catflag
About to read out the /home/hacker/not-the-flag file!
pwn.college{gYyWPWL6lRnZJNWdwUWgUrEadC4.dlTM1UDL4EzN0czW}
```
