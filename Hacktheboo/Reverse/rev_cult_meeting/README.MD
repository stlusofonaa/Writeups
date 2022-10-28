# Writeups
HackTheBoo CTF Hackthebox



# Cult Meeting
**Description:** After months of research, you're ready to attempt to infiltrate the meeting of a shadowy cult. Unfortunately, it looks like they've changed their password!

### Solution 
They give you a ELF64 and a docker with the file running asking for a password:


```python

┌──(kali㉿kali)-[~/Desktop/ctf/rev_cult_meeting]
└─$ ./meeting 
You knock on the door and a panel slides back
|/👁 👁 \| A hooded figure looks out at you
"What is the password for this week's meeting?" 
```

Simply do **strings** command and the password will popup:

```python
┌──(kali㉿kali)-[~/Desktop/ctf/rev_cult_meeting]
└─$ strings meeting 
/lib64/ld-linux-x86-64.so.2
mgUa
puts
stdin
fgets
stdout
system
fwrite
strchr
__cxa_finalize
setvbuf
strcmp
__libc_start_main
libc.so.6
GLIBC_2.2.5
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
u/UH
[]A\A]A^A_
[3mYou knock on the door and a panel slides back
[3m A hooded figure looks out at you
"What is the password for this week's meeting?" 
sup3r_s3cr3t_p455w0rd_f0r_u! #password
```
Then when you enter the password a shell will be created, do **ls** and **cat** to the flag.txt:
```python

┌──(kali㉿kali)-[~/Desktop/ctf/rev_cult_meeting]
└─$ nc 134.122.106.203 30126
You knock on the door and a panel slides back
|/👁 👁 \| A hooded figure looks out at you
"What is the password for this week's meeting?" sup3r_s3cr3t_p455w0rd_f0r_u!
sup3r_s3cr3t_p455w0rd_f0r_u!
The panel slides closed and the lock clicks
|      | "Welcome inside..." 
/bin/sh: 0: can't access tty; job control turned off
$ ls            
ls
flag.txt  meeting
$ cat flag.txt
cat flag.txt
HTB{1nf1ltr4t1ng_4_cul7_0f_str1ng5}
$ 


```



