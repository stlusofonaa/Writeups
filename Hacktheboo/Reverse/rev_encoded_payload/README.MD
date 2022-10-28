## Encoded Payload
**Description:** Buried in your basement you've discovered an ancient tome. The pages are full of what look like warnings, but luckily you can't read the language! What will happen if you invoke the ancient spells here?

### Solution 
They give you a ELF32 file but if you try to run it nothing appears:

```python
┌──(kali㉿kali)-[~/Desktop/ctf/encoded payload]
└─$ file encodedpayload 
encodedpayload: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), statically linked, no section header
```

Preety simple also, use **strace** to see imported stuff by system and the flag will appear:

```python
┌──(kali㉿kali)-[~/Desktop/ctf/encoded payload]
└─$ strace ./encodedpayload
execve("./encodedpayload", ["./encodedpayload"], 0x7ffc769bf0b0 /* 54 vars */) = 0
[ Process PID=589105 runs in 32 bit mode. ]
socket(AF_INET, SOCK_STREAM, IPPROTO_IP) = 3
dup2(3, 2)                              = 2
dup2(3, 1)                              = 1
dup2(3, 0)                              = 0
connect(3, {sa_family=AF_INET, sin_port=htons(1337), sin_addr=inet_addr("127.0.0.1")}, 102) = -1 ECONNREFUSED (Connection refused)
syscall_0xffffffffffffff0b(0xfff49888, 0xfff49880, 0, 0, 0, 0) = -1 ENOSYS (Function not implemented)
execve("/bin/sh", ["/bin/sh", "-c", "echo HTB{PLz_strace_M333}"], NULL) = 0
[ Process PID=589105 runs in 64 bit mode. ]
brk(NULL)                               = 0x564e50866000
mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7efd8e90e000
access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 4
newfstatat(4, "", {st_mode=S_IFREG|0644, st_size=78526, ...}, AT_EMPTY_PATH) = 0
mmap(NULL, 78526, PROT_READ, MAP_PRIVATE, 4, 0) = 0x7efd8e8fa000
close(4)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libc.so.6", O_RDONLY|O_CLOEXEC) = 4
read(4, "\177ELF\2\1\1\3\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\300\223\2\0\0\0\0\0"..., 832) = 832
pread64(4, "\6\0\0\0\4\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0"..., 784, 64) = 784
pread64(4, "\4\0\0\0\20\0\0\0\5\0\0\0GNU\0\2\200\0\300\4\0\0\0\1\0\0\0\0\0\0\0", 32, 848) = 32
pread64(4, "\4\0\0\0\24\0\0\0\3\0\0\0GNU\0q\247\307\271{\300\263\343I\243\330d\2ReU"..., 68, 880) = 68
newfstatat(4, "", {st_mode=S_IFREG|0755, st_size=2061320, ...}, AT_EMPTY_PATH) = 0
pread64(4, "\6\0\0\0\4\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0"..., 784, 64) = 784
mmap(NULL, 2109328, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 4, 0) = 0x7efd8e600000
mmap(0x7efd8e628000, 1507328, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 4, 0x28000) = 0x7efd8e628000
mmap(0x7efd8e798000, 360448, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 4, 0x198000) = 0x7efd8e798000
mmap(0x7efd8e7f0000, 24576, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 4, 0x1f0000) = 0x7efd8e7f0000
mmap(0x7efd8e7f6000, 53136, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x7efd8e7f6000
close(4)                                = 0
mmap(NULL, 12288, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7efd8e8f7000
arch_prctl(ARCH_SET_FS, 0x7efd8e8f7740) = 0
set_tid_address(0x7efd8e8f7a10)         = 589105
set_robust_list(0x7efd8e8f7a20, 24)     = 0
rseq(0x7efd8e8f80e0, 0x20, 0, 0x53053053) = 0
mprotect(0x7efd8e7f0000, 16384, PROT_READ) = 0
mprotect(0x564e4f93b000, 8192, PROT_READ) = 0
mprotect(0x7efd8e943000, 8192, PROT_READ) = 0
prlimit64(0, RLIMIT_STACK, NULL, {rlim_cur=8192*1024, rlim_max=RLIM64_INFINITY}) = 0
munmap(0x7efd8e8fa000, 78526)           = 0
getuid()                                = 1000
getgid()                                = 1000
getpid()                                = 589105
rt_sigaction(SIGCHLD, {sa_handler=0x564e4f930ca0, sa_mask=~[RTMIN RT_1], sa_flags=SA_RESTORER, sa_restorer=0x7efd8e63daa0}, NULL, 8) = 0
geteuid()                               = 1000
getppid()                               = 589102
getrandom("\x6e\x3e\xb2\xde\xd5\x97\x14\x64", 8, GRND_NONBLOCK) = 8
brk(NULL)                               = 0x564e50866000
brk(0x564e50887000)                     = 0x564e50887000
getcwd("/home/kali/Desktop/ctf/encoded payload", 4096) = 39
geteuid()                               = 1000
getegid()                               = 1000
rt_sigaction(SIGINT, NULL, {sa_handler=SIG_DFL, sa_mask=[], sa_flags=0}, 8) = 0
rt_sigaction(SIGINT, {sa_handler=0x564e4f930ca0, sa_mask=~[RTMIN RT_1], sa_flags=SA_RESTORER, sa_restorer=0x7efd8e63daa0}, NULL, 8) = 0
rt_sigaction(SIGQUIT, NULL, {sa_handler=SIG_DFL, sa_mask=[], sa_flags=0}, 8) = 0
rt_sigaction(SIGQUIT, {sa_handler=SIG_DFL, sa_mask=~[RTMIN RT_1], sa_flags=SA_RESTORER, sa_restorer=0x7efd8e63daa0}, NULL, 8) = 0
rt_sigaction(SIGTERM, NULL, {sa_handler=SIG_DFL, sa_mask=[], sa_flags=0}, 8) = 0
rt_sigaction(SIGTERM, {sa_handler=SIG_DFL, sa_mask=~[RTMIN RT_1], sa_flags=SA_RESTORER, sa_restorer=0x7efd8e63daa0}, NULL, 8) = 0
write(1, "HTB{PLz_strace_M333}\n", 21)  = -1 EPIPE (Broken pipe)
--- SIGPIPE {si_signo=SIGPIPE, si_code=SI_USER, si_pid=589105, si_uid=1000} ---
+++ killed by SIGPIPE +++

 ```


# Flag
```
HTB{PLz_strace_M333}
```
