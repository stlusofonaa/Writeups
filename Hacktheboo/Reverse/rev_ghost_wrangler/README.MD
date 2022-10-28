## Ghost Wrangler
**Description:** Who you gonna call?

### Solution 
They give you ELF64 file that have an empty space:

```python
┌──(kali㉿kali)-[~/Desktop/ctf/rev_ghost_wrangler]
└─$ ./ghost 
|___________________________________| I've managed to trap the flag ghost in this box, but it's turned invisible!
Can you figure out how to reveal them?
```
If we do **ltrace** with the window in fullscreen it shows a part of the flag:

```python
┌──(kali㉿kali)-[~/Desktop/ctf/rev_ghost_wrangler]
└─$ ltrace ./ghost 
malloc(41)                                                                                                                                        = 0x55b4d0a7c2a0
memset(0x55b4d0a7c2a0, '\0', 41)                                                                                                                  = 0x55b4d0a7c2a0
|                                       _| I've managed to trap the flag ghost in this box, but it's turned invisible!gh0st5_0f_ctf5_p45t!}
Can you figure out how to reveal them?
)                                              = 208
+++ exited (status 0) +++
```
If we low the size of the window it shows the other part of the flag:
```python
┌──(kali㉿kali)-[~/Desktop/ctf/rev_ghost_wrangler]
└─$ ltrace ./ghost
malloc(41)                                                                          = 0x564ad86fa2a0
memset(0x564ad86fa2a0, '\0', 41)                                                    = 0x564ad86fa2a0
printf("%s\r|\033[4m%*.c\033[24m| I've managed "..., "HTB{h4unt3d_by_th3_gh0st5_0f_ctf"..., 40, '_'HTB{h4unt3d_by_th3_gh0st5_0f_ctf5_p45t|                                       _| I've managed to trap the flag ghost in this box, but it's turned invisible!
Can you figure out how to reveal them?
) = 208
+++ exited (status 0) +++

```

# Flag
```
HTB{h4unt3d_by_th3_gh0st5_0f_ctf5_p45t!}
```
