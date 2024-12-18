# GDB baby step 1
In this challenge we have figure out what is in the `eax` register at the end of the `main` function.

## Hints given:-
1.) gdb is a very good debugger to use for this problem and many others!
2.) `main` is actually a recognized symbol that can be used with gdb commands.

The working of this problem is given below: -

Given below is the installation of `gdb` debugger.
command for it: `sudo apt install gdb`
```bash
muizz@LAPTOP-VF1FT9IQ:~$ sudo apt install gdb
[sudo] password for muizz:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libbabeltrace1 libboost-regex1.74.0 libc6-dbg libdebuginfod-common libdebuginfod1 libipt2 libsource-highlight-common libsource-highlight4v5
Suggested packages:
  gdb-doc gdbserver
The following NEW packages will be installed:
  gdb libbabeltrace1 libboost-regex1.74.0 libc6-dbg libdebuginfod-common libdebuginfod1 libipt2 libsource-highlight-common
  libsource-highlight4v5
0 upgraded, 9 newly installed, 0 to remove and 56 not upgraded.
Need to get 18.7 MB of archives.
After this operation, 35.1 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu jammy/main amd64 libdebuginfod-common all 0.186-1build1 [7878 B]
Get:2 http://archive.ubuntu.com/ubuntu jammy/main amd64 libbabeltrace1 amd64 1.5.8-2build1 [160 kB]
Get:3 http://archive.ubuntu.com/ubuntu jammy/main amd64 libdebuginfod1 amd64 0.186-1build1 [12.7 kB]
Get:4 http://archive.ubuntu.com/ubuntu jammy/main amd64 libipt2 amd64 2.0.5-1 [46.4 kB]
Get:5 http://archive.ubuntu.com/ubuntu jammy/main amd64 libsource-highlight-common all 3.1.9-4.1build2 [64.5 kB]
Get:6 http://archive.ubuntu.com/ubuntu jammy/main amd64 libboost-regex1.74.0 amd64 1.74.0-14ubuntu3 [511 kB]
Get:7 http://archive.ubuntu.com/ubuntu jammy/main amd64 libsource-highlight4v5 amd64 3.1.9-4.1build2 [207 kB]
Get:8 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 gdb amd64 12.1-0ubuntu1~22.04.2 [3920 kB]
Get:9 http://archive.ubuntu.com/ubuntu jammy-updates/main amd64 libc6-dbg amd64 2.35-0ubuntu3.8 [13.8 MB]
Fetched 18.7 MB in 3s (7232 kB/s)
Preconfiguring packages ...
Selecting previously unselected package libdebuginfod-common.
(Reading database ... 45084 files and directories currently installed.)
Preparing to unpack .../0-libdebuginfod-common_0.186-1build1_all.deb ...
Unpacking libdebuginfod-common (0.186-1build1) ...
Selecting previously unselected package libbabeltrace1:amd64.
Preparing to unpack .../1-libbabeltrace1_1.5.8-2build1_amd64.deb ...
Unpacking libbabeltrace1:amd64 (1.5.8-2build1) ...
Selecting previously unselected package libdebuginfod1:amd64.
Preparing to unpack .../2-libdebuginfod1_0.186-1build1_amd64.deb ...
Unpacking libdebuginfod1:amd64 (0.186-1build1) ...
Selecting previously unselected package libipt2.
Preparing to unpack .../3-libipt2_2.0.5-1_amd64.deb ...
Unpacking libipt2 (2.0.5-1) ...
Selecting previously unselected package libsource-highlight-common.
Preparing to unpack .../4-libsource-highlight-common_3.1.9-4.1build2_all.deb ...
Unpacking libsource-highlight-common (3.1.9-4.1build2) ...
Selecting previously unselected package libboost-regex1.74.0:amd64.
Preparing to unpack .../5-libboost-regex1.74.0_1.74.0-14ubuntu3_amd64.deb ...
Unpacking libboost-regex1.74.0:amd64 (1.74.0-14ubuntu3) ...
Selecting previously unselected package libsource-highlight4v5.
Preparing to unpack .../6-libsource-highlight4v5_3.1.9-4.1build2_amd64.deb ...
Unpacking libsource-highlight4v5 (3.1.9-4.1build2) ...
Selecting previously unselected package gdb.
Preparing to unpack .../7-gdb_12.1-0ubuntu1~22.04.2_amd64.deb ...
Unpacking gdb (12.1-0ubuntu1~22.04.2) ...
Selecting previously unselected package libc6-dbg:amd64.
Preparing to unpack .../8-libc6-dbg_2.35-0ubuntu3.8_amd64.deb ...
Unpacking libc6-dbg:amd64 (2.35-0ubuntu3.8) ...
Setting up libdebuginfod-common (0.186-1build1) ...

Creating config file /etc/profile.d/debuginfod.sh with new version

Creating config file /etc/profile.d/debuginfod.csh with new version
Setting up libdebuginfod1:amd64 (0.186-1build1) ...
Setting up libsource-highlight-common (3.1.9-4.1build2) ...
Setting up libc6-dbg:amd64 (2.35-0ubuntu3.8) ...
Setting up libboost-regex1.74.0:amd64 (1.74.0-14ubuntu3) ...
Setting up libipt2 (2.0.5-1) ...
Setting up libbabeltrace1:amd64 (1.5.8-2build1) ...
Setting up libsource-highlight4v5 (3.1.9-4.1build2) ...
Setting up gdb (12.1-0ubuntu1~22.04.2) ...
Processing triggers for man-db (2.10.2-1) ...
Processing triggers for libc-bin (2.35-0ubuntu3.8) ...
```

After that is complete, we have to use the command `gdb` following by the file name as the argument.
In this case it is `gdb debugger0_a`.
```bash
muizz@LAPTOP-VF1FT9IQ:~$ gdb debugger0_a
GNU gdb (Ubuntu 12.1-0ubuntu1~22.04.2) 12.1
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from debugger0_a...
(No debugging symbols found in debugger0_a)
(gdb)
```
Now to list all the functions running we use `info functions` in `gdb`.
```bash
muizz@LAPTOP-VF1FT9IQ:~$ gdb debugger0_a
GNU gdb (Ubuntu 12.1-0ubuntu1~22.04.2) 12.1
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from debugger0_a...
(No debugging symbols found in debugger0_a)
(gdb) info functions
All defined functions:

Non-debugging symbols:
0x0000000000001000  _init
0x0000000000001030  __cxa_finalize@plt
0x0000000000001040  _start
0x0000000000001070  deregister_tm_clones
0x00000000000010a0  register_tm_clones
0x00000000000010e0  __do_global_dtors_aux
0x0000000000001120  frame_dummy
0x0000000000001129  main
0x0000000000001140  __libc_csu_init
0x00000000000011b0  __libc_csu_fini
0x00000000000011b8  _fini
(gdb)
```
Now, the hint given to us that `main` is a recognized symbol which can be used with gdb commands.
After that we ue the command `diassemble main`.
```bash
muizz@LAPTOP-VF1FT9IQ:~$ gdb debugger0_a
GNU gdb (Ubuntu 12.1-0ubuntu1~22.04.2) 12.1
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from debugger0_a...
(No debugging symbols found in debugger0_a)
(gdb) info functions
All defined functions:

Non-debugging symbols:
0x0000000000001000  _init
0x0000000000001030  __cxa_finalize@plt
0x0000000000001040  _start
0x0000000000001070  deregister_tm_clones
0x00000000000010a0  register_tm_clones
0x00000000000010e0  __do_global_dtors_aux
0x0000000000001120  frame_dummy
0x0000000000001129  main
0x0000000000001140  __libc_csu_init
0x00000000000011b0  __libc_csu_fini
0x00000000000011b8  _fini
(gdb) disassemble main
Dump of assembler code for function main:
   0x0000000000001129 <+0>:     endbr64
   0x000000000000112d <+4>:     push   %rbp
   0x000000000000112e <+5>:     mov    %rsp,%rbp
   0x0000000000001131 <+8>:     mov    %edi,-0x4(%rbp)
   0x0000000000001134 <+11>:    mov    %rsi,-0x10(%rbp)
   0x0000000000001138 <+15>:    mov    $0x86342,%eax
   0x000000000000113d <+20>:    pop    %rbp
   0x000000000000113e <+21>:    ret
End of assembler dump.
(gdb)
```

Since we have to print the value of `eax` register, so we use to the command `print 0x86342` to `gdb`.
```bash
muizz@LAPTOP-VF1FT9IQ:~$ gdb debugger0_a
GNU gdb (Ubuntu 12.1-0ubuntu1~22.04.2) 12.1
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from debugger0_a...
(No debugging symbols found in debugger0_a)
(gdb) info functions
All defined functions:

Non-debugging symbols:
0x0000000000001000  _init
0x0000000000001030  __cxa_finalize@plt
0x0000000000001040  _start
0x0000000000001070  deregister_tm_clones
0x00000000000010a0  register_tm_clones
0x00000000000010e0  __do_global_dtors_aux
0x0000000000001120  frame_dummy
0x0000000000001129  main
0x0000000000001140  __libc_csu_init
0x00000000000011b0  __libc_csu_fini
0x00000000000011b8  _fini
(gdb) disassemble main
Dump of assembler code for function main:
   0x0000000000001129 <+0>:     endbr64
   0x000000000000112d <+4>:     push   %rbp
   0x000000000000112e <+5>:     mov    %rsp,%rbp
   0x0000000000001131 <+8>:     mov    %edi,-0x4(%rbp)
   0x0000000000001134 <+11>:    mov    %rsi,-0x10(%rbp)
   0x0000000000001138 <+15>:    mov    $0x86342,%eax
   0x000000000000113d <+20>:    pop    %rbp
   0x000000000000113e <+21>:    ret
End of assembler dump.
(gdb) print $0x86342
$1 = void
(gdb) print 0x86342
$2 = 549698
(gdb)
```
The value we get is `549698`.
Therefore, the final flag is `picoCTF{549698}`.

## References
1.) `https://visualgdb.com/gdbreference/commands/`

#
