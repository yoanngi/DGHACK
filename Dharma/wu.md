# Dharma

![dar](./darma.png)

## Wu

Nous avons un binaire de type ELF strippé. 

On ne peux pas le lancé directement dans gdb, nous avons un `int3` qui nous embète.

On peux le lancé avec strace histoire de comprendre un peu ce qu'il ce passe:
```
$strace ./dharma 
execve("./dharma", ["./dharma"], 0x7fff41e93d30 /* 47 vars */) = 0
brk(NULL)                               = 0x5646d577f000
access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=133829, ...}) = 0
mmap(NULL, 133829, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7f9f78751000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libdl.so.2", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0000\21\0\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0644, st_size=18688, ...}) = 0
mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7f9f7874f000
mmap(NULL, 20752, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7f9f78749000
mmap(0x7f9f7874a000, 8192, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1000) = 0x7f9f7874a000
mmap(0x7f9f7874c000, 4096, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x3000) = 0x7f9f7874c000
mmap(0x7f9f7874d000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x3000) = 0x7f9f7874d000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libpthread.so.0", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0 |\0\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0755, st_size=149608, ...}) = 0
mmap(NULL, 136304, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7f9f78727000
mmap(0x7f9f7872e000, 65536, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x7000) = 0x7f9f7872e000
mmap(0x7f9f7873e000, 20480, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x17000) = 0x7f9f7873e000
mmap(0x7f9f78743000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1b000) = 0x7f9f78743000
mmap(0x7f9f78745000, 13424, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x7f9f78745000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\3\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\0n\2\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0755, st_size=1839792, ...}) = 0
mmap(NULL, 1852680, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7f9f78562000
mprotect(0x7f9f78587000, 1662976, PROT_NONE) = 0
mmap(0x7f9f78587000, 1355776, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x25000) = 0x7f9f78587000
mmap(0x7f9f786d2000, 303104, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x170000) = 0x7f9f786d2000
mmap(0x7f9f7871d000, 24576, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1ba000) = 0x7f9f7871d000
mmap(0x7f9f78723000, 13576, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x7f9f78723000
close(3)                                = 0
mmap(NULL, 12288, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7f9f7855f000
arch_prctl(ARCH_SET_FS, 0x7f9f7855f740) = 0
mprotect(0x7f9f7871d000, 12288, PROT_READ) = 0
mprotect(0x7f9f78743000, 4096, PROT_READ) = 0
mprotect(0x7f9f7874d000, 4096, PROT_READ) = 0
mprotect(0x5646d4e36000, 4096, PROT_READ) = 0
mprotect(0x7f9f7879c000, 4096, PROT_READ) = 0
munmap(0x7f9f78751000, 133829)          = 0
set_tid_address(0x7f9f7855fa10)         = 107056
set_robust_list(0x7f9f7855fa20, 24)     = 0
rt_sigaction(SIGRTMIN, {sa_handler=0x7f9f7872e690, sa_mask=[], sa_flags=SA_RESTORER|SA_SIGINFO, sa_restorer=0x7f9f7873b140}, NULL, 8) = 0
rt_sigaction(SIGRT_1, {sa_handler=0x7f9f7872e730, sa_mask=[], sa_flags=SA_RESTORER|SA_RESTART|SA_SIGINFO, sa_restorer=0x7f9f7873b140}, NULL, 8) = 0
rt_sigprocmask(SIG_UNBLOCK, [RTMIN RT_1], NULL, 8) = 0
prlimit64(0, RLIMIT_STACK, NULL, {rlim_cur=8192*1024, rlim_max=RLIM64_INFINITY}) = 0
mmap(NULL, 8392704, PROT_NONE, MAP_PRIVATE|MAP_ANONYMOUS|MAP_STACK, -1, 0) = 0x7f9f77d5e000
mprotect(0x7f9f77d5f000, 8388608, PROT_READ|PROT_WRITE) = 0
brk(NULL)                               = 0x5646d577f000
brk(0x5646d57a0000)                     = 0x5646d57a0000
clone(child_stack=0x7f9f7855dfb0, flags=CLONE_VM|CLONE_FS|CLONE_FILES|CLONE_SIGHAND|CLONE_THREAD|CLONE_SYSVSEM|CLONE_SETTLS|CLONE_PARENT_SETTID|CLONE_CHILD_CLEARTID, parent_tid=[107057], tls=0x7f9f7855e700, child_tidptr=0x7f9f7855e9d0) = 107057
rt_sigaction(SIGTRAP, {sa_handler=0x5646d4e34875, sa_mask=[TRAP], sa_flags=SA_RESTORER|SA_RESTART, sa_restorer=0x7f9f7859de30}, {sa_handler=SIG_DFL, sa_mask=[], sa_flags=0}, 8) = 0
memfd_create("2O3naSbh", MFD_CLOEXEC)   = 3
write(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0 \22\0\0\0\0\0\0"..., 16936) = 16936
uname({sysname="Linux", nodename="parrot", ...}) = 0
getpid()                                = 107056
futex(0x7f9f7874e0c8, FUTEX_WAKE_PRIVATE, 2147483647) = 0
openat(AT_FDCWD, "/proc/107056/fd/3", O_RDONLY|O_CLOEXEC) = 4
read(4, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0 \22\0\0\0\0\0\0"..., 832) = 832
fstat(4, {st_mode=S_IFREG|0777, st_size=16936, ...}) = 0
mmap(NULL, 16544, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 4, 0) = 0x7f9f7876d000
mmap(0x7f9f7876e000, 4096, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 4, 0x1000) = 0x7f9f7876e000
mmap(0x7f9f7876f000, 4096, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 4, 0x2000) = 0x7f9f7876f000
mmap(0x7f9f78770000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 4, 0x2000) = 0x7f9f78770000
close(4)                                = 0
mprotect(0x7f9f78770000, 4096, PROT_READ) = 0
close(3)                                = 0
openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=133829, ...}) = 0
mmap(NULL, 133829, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7f9f77d3d000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libgcc_s.so.1", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\0203\0\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0644, st_size=100736, ...}) = 0
mmap(NULL, 103496, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x7f9f78753000
mmap(0x7f9f78756000, 69632, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x3000) = 0x7f9f78756000
mmap(0x7f9f78767000, 16384, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x14000) = 0x7f9f78767000
mmap(0x7f9f7876b000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x17000) = 0x7f9f7876b000
close(3)                                = 0
mprotect(0x7f9f7876b000, 4096, PROT_READ) = 0
munmap(0x7f9f77d3d000, 133829)          = 0
getpid()                                = 107056
tgkill(107056, 107057, SIGRTMIN)        = 0
mmap(NULL, 8392704, PROT_NONE, MAP_PRIVATE|MAP_ANONYMOUS|MAP_STACK, -1, 0) = 0x7f9f7755d000
mprotect(0x7f9f7755e000, 8388608, PROT_READ|PROT_WRITE) = 0
clone(child_stack=0x7f9f77d5cfb0, flags=CLONE_VM|CLONE_FS|CLONE_FILES|CLONE_SIGHAND|CLONE_THREAD|CLONE_SYSVSEM|CLONE_SETTLS|CLONE_PARENT_SETTID|CLONE_CHILD_CLEARTID, parent_tid=[107058], tls=0x7f9f77d5d700, child_tidptr=0x7f9f77d5d9d0) = 107058
fstat(1, {st_mode=S_IFCHR|0620, st_rdev=makedev(0x88, 0x1), ...}) = 0
write(1, "Password: \n", 11Password: 
)            = 11
fstat(0, {st_mode=S_IFCHR|0620, st_rdev=makedev(0x88, 0x1), ...}) = 0
read(0, sssss
"sssss\n", 1024)                = 6
write(1, "Nope, try again...\n", 19Nope, try again...
)    = 19
getpid()                                = 107056
tgkill(107056, 107058, SIGRTMIN)        = 0
lseek(0, -6, SEEK_CUR)                  = -1 ESPIPE (Illegal seek)
exit_group(0)                           = ?
+++ exited with 0 +++
```

On peux voir qu'il charge un programme en mémoire.

Avec une analyse statique (objdump) on peux voir aussi un appel a la lib pthread, je commence mon exploitation a ce moment la.

```
┌─[yoginet@parrot]─[~/Documents/DGHACK/DGHACK/Dharma]
└──╼ $gdb dharma 
GNU gdb (Debian 9.2-1) 9.2
Copyright (C) 2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from dharma...
(No debugging symbols found in dharma)
gdb-peda$ b*0x555555555844
Breakpoint 1 at 0x555555555844
gdb-peda$ r
Starting program: /home/yoginet/Documents/DGHACK/DGHACK/Dharma/dharma 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".
[New Thread 0x7ffff7db7700 (LWP 423292)]
[----------------------------------registers-----------------------------------]
RAX: 0x7ffff7fc8d64 (<_libc_start_main>:	endbr64)
RBX: 0x55555555c288 --> 0x7ffff7fc8d64 (<_libc_start_main>:	endbr64)
RCX: 0x0 
RDX: 0x7ffff7fc8d64 (<_libc_start_main>:	endbr64)
RSI: 0x0 
RDI: 0x55555555c278 --> 0x7ffff7db7700 (0x00007ffff7db7700)
RBP: 0x7fffffffdfb0 --> 0x7fffffffdfc0 --> 0x555555555900 (endbr64)
RSP: 0x7fffffffdf90 --> 0x7fff00000003 
RIP: 0x555555555844 (call   0x5555555551b0 <pthread_create@plt>)
R8 : 0x0 
R9 : 0x7ffff7fae1a8 --> 0xd0012000004d3 
R10: 0xfffffffffffff28d 
R11: 0x206 
R12: 0x555555555320 (endbr64)
R13: 0x0 
R14: 0x0 
R15: 0x0
EFLAGS: 0x246 (carry PARITY adjust ZERO sign trap INTERRUPT direction overflow)
[-------------------------------------code-------------------------------------]
   0x555555555835:	mov    rdx,rax
   0x555555555838:	mov    esi,0x0
   0x55555555583d:	lea    rdi,[rip+0x6a34]        # 0x55555555c278
=> 0x555555555844:	call   0x5555555551b0 <pthread_create@plt>
   0x555555555849:	mov    rax,QWORD PTR [rip+0x6a30]        # 0x55555555c280
   0x555555555850:	and    eax,0xfff
   0x555555555855:	mov    DWORD PTR [rbp-0x1c],eax
   0x555555555858:	mov    rdx,QWORD PTR [rip+0x6a21]        # 0x55555555c280
Guessed arguments:
arg[0]: 0x55555555c278 --> 0x7ffff7db7700 (0x00007ffff7db7700)
arg[1]: 0x0 
arg[2]: 0x7ffff7fc8d64 (<_libc_start_main>:	endbr64)
arg[3]: 0x0 
[------------------------------------stack-------------------------------------]
0000| 0x7fffffffdf90 --> 0x7fff00000003 
0008| 0x7fffffffdf98 --> 0x55555555d410 --> 0x7ffff7fc7000 --> 0x10102464c457f 
0016| 0x7fffffffdfa0 --> 0x0 
0024| 0x7fffffffdfa8 --> 0x0 
0032| 0x7fffffffdfb0 --> 0x7fffffffdfc0 --> 0x555555555900 (endbr64)
0040| 0x7fffffffdfb8 --> 0x5555555558e0 (mov    rax,QWORD PTR [rip+0x6991]        # 0x55555555c278)
0048| 0x7fffffffdfc0 --> 0x555555555900 (endbr64)
0056| 0x7fffffffdfc8 --> 0x7ffff7de1cca (<__libc_start_main+234>:	mov    edi,eax)
[------------------------------------------------------------------------------]
Legend: code, data, rodata, value

Thread 1 "dharma" hit Breakpoint 1, 0x0000555555555844 in ?? ()
gdb-peda$ b*0x7ffff7fc8d64
Breakpoint 2 at 0x7ffff7fc8d64
gdb-peda$ b*0x555555555849
Breakpoint 3 at 0x555555555849
gdb-peda$ handle SIG32 nostop
Signal        Stop	Print	Pass to program	Description
SIG32         No	Yes	Yes		Real-time event 32
gdb-peda$ c
Continuing.

Thread 2 "dharma" received signal SIG32, Real-time event 32.
[Thread 0x7ffff7db7700 (LWP 423292) exited]
[New Thread 0x7ffff75b6700 (LWP 423300)]
[Switching to Thread 0x7ffff75b6700 (LWP 423300)]
[----------------------------------registers-----------------------------------]
RAX: 0x7ffff7fc8d64 (<_libc_start_main>:	endbr64)
RBX: 0x0 
RCX: 0x7ffff75b6700 (0x00007ffff75b6700)
RDX: 0x3e2abd3fc046c6e2 
RSI: 0x0 
RDI: 0x0 
RBP: 0x0 
RSP: 0x7ffff75b5ef8 --> 0x7ffff7f88ea7 (<start_thread+215>:	mov    QWORD PTR fs:0x630,rax)
RIP: 0x7ffff7fc8d64 (<_libc_start_main>:	endbr64)
R8 : 0x7ffff75b6700 (0x00007ffff75b6700)
R9 : 0x7ffff75b6700 (0x00007ffff75b6700)
R10: 0x7ffff75b69d0 --> 0x67584 
R11: 0x202 
R12: 0x7fffffffdf0e --> 0x100 
R13: 0x7fffffffdf0f --> 0x1 
R14: 0x7ffff75b5fc0 --> 0x0 
R15: 0x802000
EFLAGS: 0x246 (carry PARITY adjust ZERO sign trap INTERRUPT direction overflow)
[-------------------------------------code-------------------------------------]
   0x7ffff7fc8d5d <init+221>:	call   0x7ffff7fc8160 <__stack_chk_fail@plt>
   0x7ffff7fc8d62 <init+226>:	leave  
   0x7ffff7fc8d63 <init+227>:	ret    
=> 0x7ffff7fc8d64 <_libc_start_main>:	endbr64 
   0x7ffff7fc8d68 <_libc_start_main+4>:	push   rbp
   0x7ffff7fc8d69 <_libc_start_main+5>:	mov    rbp,rsp
   0x7ffff7fc8d6c <_libc_start_main+8>:	sub    rsp,0x10
   0x7ffff7fc8d70 <_libc_start_main+12>:	mov    QWORD PTR [rbp-0x8],rdi
[------------------------------------stack-------------------------------------]
0000| 0x7ffff75b5ef8 --> 0x7ffff7f88ea7 (<start_thread+215>:	mov    QWORD PTR fs:0x630,rax)
0008| 0x7ffff75b5f00 --> 0x0 
0016| 0x7ffff75b5f08 --> 0x7ffff75b6700 (0x00007ffff75b6700)
0024| 0x7ffff75b5f10 --> 0x7ffff75b6700 (0x00007ffff75b6700)
0032| 0x7ffff75b5f18 --> 0xc1d553897e46c6e2 
0040| 0x7ffff75b5f20 --> 0x7fffffffdf0e --> 0x100 
0048| 0x7ffff75b5f28 --> 0x7fffffffdf0f --> 0x1 
0056| 0x7ffff75b5f30 --> 0x7ffff75b5fc0 --> 0x0 
[------------------------------------------------------------------------------]
Legend: code, data, rodata, value

BFD: reopening /proc/423288/fd/3: No such file or directory

BFD: reopening /proc/423288/fd/3: No such file or directory

BFD: reopening /proc/423288/fd/3: No such file or directory

Thread 3 "dharma" hit Breakpoint 2, warning: Can't read data for section '.eh_frame' in file '/proc/423288/fd/3'
0x00007ffff7fc8d64 in _libc_start_main () from /proc/423288/fd/3
gdb-peda$ x/50i 0x7ffff7fc8d64
=> 0x7ffff7fc8d64 <_libc_start_main>:	endbr64 
   0x7ffff7fc8d68 <_libc_start_main+4>:	push   rbp
   0x7ffff7fc8d69 <_libc_start_main+5>:	mov    rbp,rsp
   0x7ffff7fc8d6c <_libc_start_main+8>:	sub    rsp,0x10
   0x7ffff7fc8d70 <_libc_start_main+12>:	mov    QWORD PTR [rbp-0x8],rdi
   0x7ffff7fc8d74 <_libc_start_main+16>:	int3   
   0x7ffff7fc8d75 <_libc_start_main+17>:	mov    edi,0x3e8
   0x7ffff7fc8d7a <_libc_start_main+22>:	call   0x7ffff7fc8210 <usleep@plt>
   0x7ffff7fc8d7f <_libc_start_main+27>:	jmp    0x7ffff7fc8d74 <_libc_start_main+16>
   0x7ffff7fc8d81:	add    BYTE PTR [rax],al
   0x7ffff7fc8d83:	add    bl,dh
   0x7ffff7fc8d85 <_fini+1>:	nop    edx
   0x7ffff7fc8d88 <_fini+4>:	sub    rsp,0x8
   0x7ffff7fc8d8c <_fini+8>:	add    rsp,0x8
   0x7ffff7fc8d90 <_fini+12>:	ret    
   0x7ffff7fc8d91:	add    BYTE PTR [rax],al
   0x7ffff7fc8d93:	add    BYTE PTR [rax],al
   0x7ffff7fc8d95:	add    BYTE PTR [rax],al
   0x7ffff7fc8d97:	add    BYTE PTR [rax],al
   0x7ffff7fc8d99:	add    BYTE PTR [rax],al
   0x7ffff7fc8d9b:	add    BYTE PTR [rax],al
   0x7ffff7fc8d9d:	add    BYTE PTR [rax],al
   0x7ffff7fc8d9f:	add    BYTE PTR [rax],al
   0x7ffff7fc8da1:	add    BYTE PTR [rax],al
   0x7ffff7fc8da3:	add    BYTE PTR [rax],al
   0x7ffff7fc8da5:	add    BYTE PTR [rax],al
   0x7ffff7fc8da7:	add    BYTE PTR [rax],al
   0x7ffff7fc8da9:	add    BYTE PTR [rax],al
   0x7ffff7fc8dab:	add    BYTE PTR [rax],al
   0x7ffff7fc8dad:	add    BYTE PTR [rax],al
   0x7ffff7fc8daf:	add    BYTE PTR [rax],al
   0x7ffff7fc8db1:	add    BYTE PTR [rax],al
   0x7ffff7fc8db3:	add    BYTE PTR [rax],al
   0x7ffff7fc8db5:	add    BYTE PTR [rax],al
   0x7ffff7fc8db7:	add    BYTE PTR [rax],al
   0x7ffff7fc8db9:	add    BYTE PTR [rax],al
   0x7ffff7fc8dbb:	add    BYTE PTR [rax],al
   0x7ffff7fc8dbd:	add    BYTE PTR [rax],al
   0x7ffff7fc8dbf:	add    BYTE PTR [rax],al
   0x7ffff7fc8dc1:	add    BYTE PTR [rax],al
   0x7ffff7fc8dc3:	add    BYTE PTR [rax],al
   0x7ffff7fc8dc5:	add    BYTE PTR [rax],al
   0x7ffff7fc8dc7:	add    BYTE PTR [rax],al
   0x7ffff7fc8dc9:	add    BYTE PTR [rax],al
   0x7ffff7fc8dcb:	add    BYTE PTR [rax],al
   0x7ffff7fc8dcd:	add    BYTE PTR [rax],al
   0x7ffff7fc8dcf:	add    BYTE PTR [rax],al
   0x7ffff7fc8dd1:	add    BYTE PTR [rax],al
   0x7ffff7fc8dd3:	add    BYTE PTR [rax],al
   0x7ffff7fc8dd5:	add    BYTE PTR [rax],al
gdb-peda$ skip 0x7ffff7fc8d74
Function 0x7ffff7fc8d74 will be skipped when stepping.
gdb-peda$ thread 1
[Switching to thread 1 (Thread 0x7ffff7db8740 (LWP 423288))]
#0  0x0000555555555849 in ?? ()
gdb-peda$ c
Continuing.
[----------------------------------registers-----------------------------------]
RAX: 0x0 
RBX: 0x55555555c288 --> 0x7ffff7fc8d64 (<_libc_start_main>:	endbr64)
RCX: 0x0 
RDX: 0x0 
RSI: 0x7ffff75b5fb0 --> 0x7fffffffdf0e --> 0x100 
RDI: 0x3d0f00 
RBP: 0x7fffffffdfb0 --> 0x7fffffffdfc0 --> 0x555555555900 (endbr64)
RSP: 0x7fffffffdf90 --> 0x7fff00000003 
RIP: 0x555555555849 (mov    rax,QWORD PTR [rip+0x6a30]        # 0x55555555c280)
R8 : 0x7ffff75b6700 (0x00007ffff75b6700)
R9 : 0x7ffff75b6700 (0x00007ffff75b6700)
R10: 0x7ffff75b69d0 --> 0x67584 
R11: 0x202 
R12: 0x555555555320 (endbr64)
R13: 0x0 
R14: 0x0 
R15: 0x0
EFLAGS: 0x246 (carry PARITY adjust ZERO sign trap INTERRUPT direction overflow)
[-------------------------------------code-------------------------------------]
   0x555555555838:	mov    esi,0x0
   0x55555555583d:	lea    rdi,[rip+0x6a34]        # 0x55555555c278
   0x555555555844:	call   0x5555555551b0 <pthread_create@plt>
=> 0x555555555849:	mov    rax,QWORD PTR [rip+0x6a30]        # 0x55555555c280
   0x555555555850:	and    eax,0xfff
   0x555555555855:	mov    DWORD PTR [rbp-0x1c],eax
   0x555555555858:	mov    rdx,QWORD PTR [rip+0x6a21]        # 0x55555555c280
   0x55555555585f:	mov    eax,DWORD PTR [rbp-0x1c]
[------------------------------------stack-------------------------------------]
0000| 0x7fffffffdf90 --> 0x7fff00000003 
0008| 0x7fffffffdf98 --> 0x55555555d410 --> 0x7ffff7fc7000 --> 0x10102464c457f 
0016| 0x7fffffffdfa0 --> 0x0 
0024| 0x7fffffffdfa8 --> 0x0 
0032| 0x7fffffffdfb0 --> 0x7fffffffdfc0 --> 0x555555555900 (endbr64)
0040| 0x7fffffffdfb8 --> 0x5555555558e0 (mov    rax,QWORD PTR [rip+0x6991]        # 0x55555555c278)
0048| 0x7fffffffdfc0 --> 0x555555555900 (endbr64)
0056| 0x7fffffffdfc8 --> 0x7ffff7de1cca (<__libc_start_main+234>:	mov    edi,eax)
[------------------------------------------------------------------------------]
Legend: code, data, rodata, value

Thread 1 "dharma" hit Breakpoint 3, 0x0000555555555849 in ?? ()
gdb-peda$ x/30i 0x555555555849
=> 0x555555555849:	mov    rax,QWORD PTR [rip+0x6a30]        # 0x55555555c280
   0x555555555850:	and    eax,0xfff
   0x555555555855:	mov    DWORD PTR [rbp-0x1c],eax
   0x555555555858:	mov    rdx,QWORD PTR [rip+0x6a21]        # 0x55555555c280
   0x55555555585f:	mov    eax,DWORD PTR [rbp-0x1c]
   0x555555555862:	mov    esi,eax
   0x555555555864:	lea    rdi,[rip+0xfffffffffffffe6b]        # 0x5555555556d6
   0x55555555586b:	call   rdx
   0x55555555586d:	nop
   0x55555555586e:	add    rsp,0x18
   0x555555555872:	pop    rbx
   0x555555555873:	pop    rbp
   0x555555555874:	ret    
   0x555555555875:	endbr64 
   0x555555555879:	push   rbp
   0x55555555587a:	mov    rbp,rsp
   0x55555555587d:	mov    DWORD PTR [rbp-0x4],edi
   0x555555555880:	nop
   0x555555555881:	pop    rbp
   0x555555555882:	ret    
   0x555555555883:	endbr64 
   0x555555555887:	push   rbp
   0x555555555888:	mov    rbp,rsp
   0x55555555588b:	sub    rsp,0x10
   0x55555555588f:	mov    QWORD PTR [rbp-0x8],rdi
   0x555555555893:	nop
   0x555555555894:	mov    edi,0x3e8
   0x555555555899:	call   0x555555555310 <usleep@plt>
   0x55555555589e:	jmp    0x555555555893
   0x5555555558a0:	endbr64 
gdb-peda$ b*0x55555555586b
Breakpoint 4 at 0x55555555586b
gdb-peda$ info skip 
Num   Enb Glob File                 RE Function
1     y      n <none>                n 0x7ffff7fc8d74
gdb-peda$ c
Continuing.

Thread 3 "dharma" received signal SIGTRAP, Trace/breakpoint trap.
[Switching to Thread 0x7ffff75b6700 (LWP 423300)]
[----------------------------------registers-----------------------------------]
RAX: 0x7ffff7fc8d64 (<_libc_start_main>:	endbr64)
RBX: 0x0 
RCX: 0x7ffff75b6700 (0x00007ffff75b6700)
RDX: 0x3e2abd3fc046c6e2 
RSI: 0x0 
RDI: 0x0 
RBP: 0x7ffff75b5ef0 --> 0x0 
RSP: 0x7ffff75b5ee0 --> 0x0 
RIP: 0x7ffff7fc8d75 (<_libc_start_main+17>:	mov    edi,0x3e8)
R8 : 0x7ffff75b6700 (0x00007ffff75b6700)
R9 : 0x7ffff75b6700 (0x00007ffff75b6700)
R10: 0x7ffff75b69d0 --> 0x67584 
R11: 0x202 
R12: 0x7fffffffdf0e --> 0x100 
R13: 0x7fffffffdf0f --> 0x1 
R14: 0x7ffff75b5fc0 --> 0x0 
R15: 0x802000
EFLAGS: 0x202 (carry parity adjust zero sign trap INTERRUPT direction overflow)
[-------------------------------------code-------------------------------------]
   0x7ffff7fc8d6c <_libc_start_main+8>:	sub    rsp,0x10
   0x7ffff7fc8d70 <_libc_start_main+12>:	mov    QWORD PTR [rbp-0x8],rdi
   0x7ffff7fc8d74 <_libc_start_main+16>:	int3   
=> 0x7ffff7fc8d75 <_libc_start_main+17>:	mov    edi,0x3e8
   0x7ffff7fc8d7a <_libc_start_main+22>:	call   0x7ffff7fc8210 <usleep@plt>
   0x7ffff7fc8d7f <_libc_start_main+27>:	jmp    0x7ffff7fc8d74 <_libc_start_main+16>
   0x7ffff7fc8d81:	add    BYTE PTR [rax],al
   0x7ffff7fc8d83:	add    bl,dh
[------------------------------------stack-------------------------------------]
0000| 0x7ffff75b5ee0 --> 0x0 
0008| 0x7ffff75b5ee8 --> 0x0 
0016| 0x7ffff75b5ef0 --> 0x0 
0024| 0x7ffff75b5ef8 --> 0x7ffff7f88ea7 (<start_thread+215>:	mov    QWORD PTR fs:0x630,rax)
0032| 0x7ffff75b5f00 --> 0x0 
0040| 0x7ffff75b5f08 --> 0x7ffff75b6700 (0x00007ffff75b6700)
0048| 0x7ffff75b5f10 --> 0x7ffff75b6700 (0x00007ffff75b6700)
0056| 0x7ffff75b5f18 --> 0xc1d553897e46c6e2 
[------------------------------------------------------------------------------]
Legend: code, data, rodata, value
Stopped reason: SIGTRAP
0x00007ffff7fc8d75 in _libc_start_main () from /proc/423288/fd/3
gdb-peda$ thread 1
[Switching to thread 1 (Thread 0x7ffff7db8740 (LWP 423288))]
#0  0x000055555555586b in ?? ()
gdb-peda$ c
Continuing.
[----------------------------------registers-----------------------------------]
RAX: 0xc80 
RBX: 0x55555555c288 --> 0x7ffff7fc8d64 (<_libc_start_main>:	endbr64)
RCX: 0x0 
RDX: 0x7ffff7fc8c80 (<init>:	endbr64)
RSI: 0xc80 
RDI: 0x5555555556d6 (endbr64)
RBP: 0x7fffffffdfb0 --> 0x7fffffffdfc0 --> 0x555555555900 (endbr64)
RSP: 0x7fffffffdf90 --> 0xc8000000003 
RIP: 0x55555555586b (call   rdx)
R8 : 0x7ffff75b6700 (0x00007ffff75b6700)
R9 : 0x7ffff75b6700 (0x00007ffff75b6700)
R10: 0x7ffff75b69d0 --> 0x67584 
R11: 0x202 
R12: 0x555555555320 (endbr64)
R13: 0x0 
R14: 0x0 
R15: 0x0
EFLAGS: 0x202 (carry parity adjust zero sign trap INTERRUPT direction overflow)
[-------------------------------------code-------------------------------------]
   0x55555555585f:	mov    eax,DWORD PTR [rbp-0x1c]
   0x555555555862:	mov    esi,eax
   0x555555555864:	lea    rdi,[rip+0xfffffffffffffe6b]        # 0x5555555556d6
=> 0x55555555586b:	call   rdx
   0x55555555586d:	nop
   0x55555555586e:	add    rsp,0x18
   0x555555555872:	pop    rbx
   0x555555555873:	pop    rbp
Guessed arguments:
arg[0]: 0x5555555556d6 (endbr64)
arg[1]: 0xc80 
arg[2]: 0x7ffff7fc8c80 (<init>:	endbr64)
[------------------------------------stack-------------------------------------]
0000| 0x7fffffffdf90 --> 0xc8000000003 
0008| 0x7fffffffdf98 --> 0x55555555d410 --> 0x7ffff7fc7000 --> 0x10102464c457f 
0016| 0x7fffffffdfa0 --> 0x0 
0024| 0x7fffffffdfa8 --> 0x0 
0032| 0x7fffffffdfb0 --> 0x7fffffffdfc0 --> 0x555555555900 (endbr64)
0040| 0x7fffffffdfb8 --> 0x5555555558e0 (mov    rax,QWORD PTR [rip+0x6991]        # 0x55555555c278)
0048| 0x7fffffffdfc0 --> 0x555555555900 (endbr64)
0056| 0x7fffffffdfc8 --> 0x7ffff7de1cca (<__libc_start_main+234>:	mov    edi,eax)
[------------------------------------------------------------------------------]
Legend: code, data, rodata, value

Thread 1 "dharma" hit Breakpoint 4, 0x000055555555586b in ?? ()
gdb-peda$ x/50i 0x7ffff7fc8c80
   0x7ffff7fc8c80 <init>:	endbr64 
   0x7ffff7fc8c84 <init+4>:	push   rbp
   0x7ffff7fc8c85 <init+5>:	mov    rbp,rsp
   0x7ffff7fc8c88 <init+8>:	sub    rsp,0x30
   0x7ffff7fc8c8c <init+12>:	mov    QWORD PTR [rbp-0x28],rdi
   0x7ffff7fc8c90 <init+16>:	mov    DWORD PTR [rbp-0x2c],esi
   0x7ffff7fc8c93 <init+19>:	mov    rax,QWORD PTR fs:0x28
   0x7ffff7fc8c9c <init+28>:	mov    QWORD PTR [rbp-0x8],rax
   0x7ffff7fc8ca0 <init+32>:	xor    eax,eax
   0x7ffff7fc8ca2 <init+34>:	mov    rdx,QWORD PTR [rbp-0x28]
   0x7ffff7fc8ca6 <init+38>:	mov    eax,0x0
   0x7ffff7fc8cab <init+43>:	call   rdx
   0x7ffff7fc8cad <init+45>:	mov    QWORD PTR [rbp-0x10],rax
   0x7ffff7fc8cb1 <init+49>:	lea    rdi,[rip+0x451]        # 0x7ffff7fc9109
   0x7ffff7fc8cb8 <init+56>:	call   0x7ffff7fc8140 <puts@plt>
   0x7ffff7fc8cbd <init+61>:	lea    rax,[rbp-0x18]
   0x7ffff7fc8cc1 <init+65>:	mov    rsi,rax
   0x7ffff7fc8cc4 <init+68>:	lea    rdi,[rip+0x43a]        # 0x7ffff7fc9105
   0x7ffff7fc8ccb <init+75>:	mov    eax,0x0
   0x7ffff7fc8cd0 <init+80>:	call   0x7ffff7fc81d0 <__isoc99_scanf@plt>
   0x7ffff7fc8cd5 <init+85>:	mov    eax,DWORD PTR [rbp-0x2c]
   0x7ffff7fc8cd8 <init+88>:	cdqe   
   0x7ffff7fc8cda <init+90>:	mov    edx,DWORD PTR [rbp-0x2c]
   0x7ffff7fc8cdd <init+93>:	movsxd rdx,edx
   0x7ffff7fc8ce0 <init+96>:	mov    rcx,rdx
   0x7ffff7fc8ce3 <init+99>:	and    ecx,0x42
   0x7ffff7fc8ce6 <init+102>:	mov    rdx,QWORD PTR [rbp-0x18]
   0x7ffff7fc8cea <init+106>:	xor    rdx,rcx
   0x7ffff7fc8ced <init+109>:	imul   rax,rdx
   0x7ffff7fc8cf1 <init+113>:	mov    rdx,QWORD PTR [rbp-0x10]
   0x7ffff7fc8cf5 <init+117>:	add    rdx,0x4
   0x7ffff7fc8cf9 <init+121>:	mov    edx,DWORD PTR [rdx]
   0x7ffff7fc8cfb <init+123>:	movsxd rsi,edx
   0x7ffff7fc8cfe <init+126>:	cqo    
   0x7ffff7fc8d00 <init+128>:	idiv   rsi
   0x7ffff7fc8d03 <init+131>:	mov    rdx,rax
   0x7ffff7fc8d06 <init+134>:	mov    rax,QWORD PTR [rbp-0x10]
   0x7ffff7fc8d0a <init+138>:	mov    eax,DWORD PTR [rax]
   0x7ffff7fc8d0c <init+140>:	cdqe   
   0x7ffff7fc8d0e <init+142>:	cmp    rdx,rax
   0x7ffff7fc8d11 <init+145>:	jne    0x7ffff7fc8d41 <init+193>
   0x7ffff7fc8d13 <init+147>:	mov    rax,QWORD PTR [rbp-0x18]
   0x7ffff7fc8d17 <init+151>:	movzx  eax,ax
   0x7ffff7fc8d1a <init+154>:	cmp    rax,0xfb4c
   0x7ffff7fc8d20 <init+160>:	jne    0x7ffff7fc8d41 <init+193>
   0x7ffff7fc8d22 <init+162>:	lea    rdi,[rip+0x3eb]        # 0x7ffff7fc9114
   0x7ffff7fc8d29 <init+169>:	mov    eax,0x0
   0x7ffff7fc8d2e <init+174>:	call   0x7ffff7fc8170 <printf@plt>
   0x7ffff7fc8d33 <init+179>:	mov    rax,QWORD PTR [rbp-0x18]
   0x7ffff7fc8d37 <init+183>:	mov    rdi,rax
gdb-peda$ b*0x7ffff7fc8cd0
Breakpoint 5 at 0x7ffff7fc8cd0
gdb-peda$ b*0x7ffff7fc8cd5
Breakpoint 6 at 0x7ffff7fc8cd5
gdb-peda$ b*0x7ffff7fc8d0e
Breakpoint 7 at 0x7ffff7fc8d0e
gdb-peda$ b*0x7ffff7fc8d1a
Breakpoint 8 at 0x7ffff7fc8d1a
gdb-peda$ b*0x7ffff7fc8d2e
Breakpoint 9 at 0x7ffff7fc8d2e
gdb-peda$ x/s 0x7ffff7fc9114
0x7ffff7fc9114:	"Yes !\nHere is your flag: "
gdb-peda$ c
Continuing.
Password: 

Thread 3 "dharma" received signal SIGTRAP, Trace/breakpoint trap.
[Switching to Thread 0x7ffff75b6700 (LWP 423300)]
[----------------------------------registers-----------------------------------]
RAX: 0x0 
RBX: 0x0 
RCX: 0x0 
RDX: 0x0 
RSI: 0x0 
RDI: 0x0 
RBP: 0x7ffff75b5ef0 --> 0x0 
RSP: 0x7ffff75b5ee0 --> 0x0 
RIP: 0x7ffff7fc8d75 (<_libc_start_main+17>:	mov    edi,0x3e8)
R8 : 0x0 
R9 : 0x7ffff75b6700 (0x00007ffff75b6700)
R10: 0x0 
R11: 0x0 
R12: 0x7fffffffdf0e --> 0x7ffff7fc91090000 
R13: 0x7fffffffdf0f --> 0x7ffff7fc910900 
R14: 0x7ffff75b5fc0 --> 0x0 
R15: 0x802000
EFLAGS: 0x206 (carry PARITY adjust zero sign trap INTERRUPT direction overflow)
[-------------------------------------code-------------------------------------]
   0x7ffff7fc8d6c <_libc_start_main+8>:	sub    rsp,0x10
   0x7ffff7fc8d70 <_libc_start_main+12>:	mov    QWORD PTR [rbp-0x8],rdi
   0x7ffff7fc8d74 <_libc_start_main+16>:	int3   
=> 0x7ffff7fc8d75 <_libc_start_main+17>:	mov    edi,0x3e8
   0x7ffff7fc8d7a <_libc_start_main+22>:	call   0x7ffff7fc8210 <usleep@plt>
   0x7ffff7fc8d7f <_libc_start_main+27>:	jmp    0x7ffff7fc8d74 <_libc_start_main+16>
   0x7ffff7fc8d81:	add    BYTE PTR [rax],al
   0x7ffff7fc8d83:	add    bl,dh
[------------------------------------stack-------------------------------------]
0000| 0x7ffff75b5ee0 --> 0x0 
0008| 0x7ffff75b5ee8 --> 0x0 
0016| 0x7ffff75b5ef0 --> 0x0 
0024| 0x7ffff75b5ef8 --> 0x7ffff7f88ea7 (<start_thread+215>:	mov    QWORD PTR fs:0x630,rax)
0032| 0x7ffff75b5f00 --> 0x0 
0040| 0x7ffff75b5f08 --> 0x7ffff75b6700 (0x00007ffff75b6700)
0048| 0x7ffff75b5f10 --> 0x7ffff75b6700 (0x00007ffff75b6700)
0056| 0x7ffff75b5f18 --> 0xc1d553897e46c6e2 
[------------------------------------------------------------------------------]
Legend: code, data, rodata, value
Stopped reason: SIGTRAP
0x00007ffff7fc8d75 in _libc_start_main () from /proc/423288/fd/3
gdb-peda$ thread 1
[Switching to thread 1 (Thread 0x7ffff7db8740 (LWP 423288))]
#0  0x00007ffff7fc8cd0 in init () from /proc/423288/fd/3
gdb-peda$ c
Continuing.
[----------------------------------registers-----------------------------------]
RAX: 0x0 
RBX: 0x55555555c288 --> 0x7ffff7fc8d64 (<_libc_start_main>:	endbr64)
RCX: 0x7ffff7ea9ecf (<__GI___libc_write+79>:	cmp    rax,0xfffffffffffff000)
RDX: 0x1 
RSI: 0x7fffffffdf68 --> 0x0 
RDI: 0x7ffff7fc9105 --> 0x7373615000646c25 ('%ld')
RBP: 0x7fffffffdf80 --> 0x7fffffffdfb0 --> 0x7fffffffdfc0 --> 0x555555555900 (endbr64)
RSP: 0x7fffffffdf50 --> 0xc8055555817 
RIP: 0x7ffff7fc8cd0 (<init+80>:	call   0x7ffff7fc81d0 <__isoc99_scanf@plt>)
R8 : 0xb ('\x0b')
R9 : 0x7ffff7f79be0 --> 0x55555555e5c0 --> 0x0 
R10: 0x6e ('n')
R11: 0x0 
R12: 0x555555555320 (endbr64)
R13: 0x0 
R14: 0x0 
R15: 0x0
EFLAGS: 0x246 (carry PARITY adjust ZERO sign trap INTERRUPT direction overflow)
[-------------------------------------code-------------------------------------]
   0x7ffff7fc8cc1 <init+65>:	mov    rsi,rax
   0x7ffff7fc8cc4 <init+68>:	lea    rdi,[rip+0x43a]        # 0x7ffff7fc9105
   0x7ffff7fc8ccb <init+75>:	mov    eax,0x0
=> 0x7ffff7fc8cd0 <init+80>:	call   0x7ffff7fc81d0 <__isoc99_scanf@plt>
   0x7ffff7fc8cd5 <init+85>:	mov    eax,DWORD PTR [rbp-0x2c]
   0x7ffff7fc8cd8 <init+88>:	cdqe   
   0x7ffff7fc8cda <init+90>:	mov    edx,DWORD PTR [rbp-0x2c]
   0x7ffff7fc8cdd <init+93>:	movsxd rdx,edx
Guessed arguments:
arg[0]: 0x7ffff7fc9105 --> 0x7373615000646c25 ('%ld')
arg[1]: 0x7fffffffdf68 --> 0x0 
[------------------------------------stack-------------------------------------]
0000| 0x7fffffffdf50 --> 0xc8055555817 
0008| 0x7fffffffdf58 --> 0x5555555556d6 (endbr64)
0016| 0x7fffffffdf60 --> 0x555555555320 (endbr64)
0024| 0x7fffffffdf68 --> 0x0 
0032| 0x7fffffffdf70 --> 0x55555555c270 ("2O3naSbh")
0040| 0x7fffffffdf78 --> 0x1d532ddfbc87e400 
0048| 0x7fffffffdf80 --> 0x7fffffffdfb0 --> 0x7fffffffdfc0 --> 0x555555555900 (endbr64)
0056| 0x7fffffffdf88 --> 0x55555555586d (nop)
[------------------------------------------------------------------------------]
Legend: code, data, rodata, value

Thread 1 "dharma" hit Breakpoint 5, 0x00007ffff7fc8cd0 in init () from /proc/423288/fd/3
```

Le code qui nous intéresse est celui ci:
```
=> 0x7ffff7fc8c80 <init>:	endbr64 
   0x7ffff7fc8c84 <init+4>:	push   rbp
   0x7ffff7fc8c85 <init+5>:	mov    rbp,rsp
   0x7ffff7fc8c88 <init+8>:	sub    rsp,0x30
   0x7ffff7fc8c8c <init+12>:	mov    QWORD PTR [rbp-0x28],rdi
   0x7ffff7fc8c90 <init+16>:	mov    DWORD PTR [rbp-0x2c],esi
   0x7ffff7fc8c93 <init+19>:	mov    rax,QWORD PTR fs:0x28
   0x7ffff7fc8c9c <init+28>:	mov    QWORD PTR [rbp-0x8],rax
   0x7ffff7fc8ca0 <init+32>:	xor    eax,eax
   0x7ffff7fc8ca2 <init+34>:	mov    rdx,QWORD PTR [rbp-0x28]
   0x7ffff7fc8ca6 <init+38>:	mov    eax,0x0
   0x7ffff7fc8cab <init+43>:	call   rdx
   0x7ffff7fc8cad <init+45>:	mov    QWORD PTR [rbp-0x10],rax
   0x7ffff7fc8cb1 <init+49>:	lea    rdi,[rip+0x451]        # 0x7ffff7fc9109
   0x7ffff7fc8cb8 <init+56>:	call   0x7ffff7fc8140 <puts@plt>
   0x7ffff7fc8cbd <init+61>:	lea    rax,[rbp-0x18]
   0x7ffff7fc8cc1 <init+65>:	mov    rsi,rax
   0x7ffff7fc8cc4 <init+68>:	lea    rdi,[rip+0x43a]        # 0x7ffff7fc9105
   0x7ffff7fc8ccb <init+75>:	mov    eax,0x0
   0x7ffff7fc8cd0 <init+80>:	call   0x7ffff7fc81d0 <__isoc99_scanf@plt>
   0x7ffff7fc8cd5 <init+85>:	mov    eax,DWORD PTR [rbp-0x2c]
   0x7ffff7fc8cd8 <init+88>:	cdqe   
   0x7ffff7fc8cda <init+90>:	mov    edx,DWORD PTR [rbp-0x2c]
   0x7ffff7fc8cdd <init+93>:	movsxd rdx,edx
   0x7ffff7fc8ce0 <init+96>:	mov    rcx,rdx
   0x7ffff7fc8ce3 <init+99>:	and    ecx,0x42
   0x7ffff7fc8ce6 <init+102>:	mov    rdx,QWORD PTR [rbp-0x18]
   0x7ffff7fc8cea <init+106>:	xor    rdx,rcx
   0x7ffff7fc8ced <init+109>:	imul   rax,rdx
   0x7ffff7fc8cf1 <init+113>:	mov    rdx,QWORD PTR [rbp-0x10]
   0x7ffff7fc8cf5 <init+117>:	add    rdx,0x4
   0x7ffff7fc8cf9 <init+121>:	mov    edx,DWORD PTR [rdx]
   0x7ffff7fc8cfb <init+123>:	movsxd rsi,edx
   0x7ffff7fc8cfe <init+126>:	cqo    
   0x7ffff7fc8d00 <init+128>:	idiv   rsi
   0x7ffff7fc8d03 <init+131>:	mov    rdx,rax
   0x7ffff7fc8d06 <init+134>:	mov    rax,QWORD PTR [rbp-0x10]
   0x7ffff7fc8d0a <init+138>:	mov    eax,DWORD PTR [rax]
   0x7ffff7fc8d0c <init+140>:	cdqe   
   0x7ffff7fc8d0e <init+142>:	cmp    rdx,rax
   0x7ffff7fc8d11 <init+145>:	jne    0x7ffff7fc8d41 <init+193>
   0x7ffff7fc8d13 <init+147>:	mov    rax,QWORD PTR [rbp-0x18]
   0x7ffff7fc8d17 <init+151>:	movzx  eax,ax
   0x7ffff7fc8d1a <init+154>:	cmp    rax,0xfb4c
   0x7ffff7fc8d20 <init+160>:	jne    0x7ffff7fc8d41 <init+193>
   0x7ffff7fc8d22 <init+162>:	lea    rdi,[rip+0x3eb]        # 0x7ffff7fc9114
   0x7ffff7fc8d29 <init+169>:	mov    eax,0x0
   0x7ffff7fc8d2e <init+174>:	call   0x7ffff7fc8170 <printf@plt>
   0x7ffff7fc8d33 <init+179>:	mov    rax,QWORD PTR [rbp-0x18]
   0x7ffff7fc8d37 <init+183>:	mov    rdi,rax
   [...]
```

C'est a cette endroit que les comparaisons sont faite pour lancé avant l'appel a printf qui nous dit que nous avons réussi.

Je n'ai pas eu le temps de terminé :/

