# Module 10 : # Untangling Users
## Challenge 1 : Becoming root with su
In this we need to switch user using `su` using the password `hack-the-planet` and read the flag
```bash
hacker@users~becoming-root-with-su:~$ su
Password: hack-the-planet
root@users~becoming-root-with-su:/home/hacker# cat /flag
pwn.college{kPSCIBE7uZJJ4ZHqcO45Db3Fvoo.dVTN0UDL4EzN0czW}
```
## Challenge 2 : Other users with su
In this challenge, we need to switch the user to `zardus` using `su` with password `dont-hack-me` and then run `/challenge/run`
```bash
hacker@users~other-users-with-su:~$ su zardus
Password: dont-hack-me
zardus@users~other-users-with-su:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{0HhwZcqqQFPlLK5EUe40BDc9wPS.dZTN0UDL4EzN0czW}
```
## Challenge 3 : Cracking Passwords
In this challenge we need to retrieve the password in `/challenge/shadow-leak` using `John the Ripper` , then use it switch the user to `zardus` using `su` and then run `/challenge/run` to get the flag.
```bash
hacker@users~cracking-passwords:~$ john /challenge/shadow-leak
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
aardvark         (zardus)
1g 0:00:00:20 100% 2/3 0.04921g/s 286.5p/s 286.5c/s 286.5C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
``` 
Now we know the password is `aardvark`, now we'll use this password to switch user to `zardus`.
```bash
hacker@users~cracking-passwords:~$ su zardus
Password: aardvark
zardus@users~cracking-passwords:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{gfqKGmeEGOaUnfMmfcK9IyG9zsY.ddTN0UDL4EzN0czW}
```
## Challenge 4 : Using sudo
In this we'll read the flag using `sudo`
```bash
hacker@users~using-sudo:~$ sudo cat /flag
pwn.college{seDxvZtSJkqdf83EVgNOIqLV6Lx.dhTN0UDL4EzN0czW}
```

