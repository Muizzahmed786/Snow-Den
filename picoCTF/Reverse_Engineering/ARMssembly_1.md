# ARMssembly 1
In this challenge we have find the value of the argument such the program prints `win` with variables `85`,`6` and `3`.
File given to us :- `https://mercury.picoctf.net/static/56a2cea908a525745578feff8b94719f/chall_1.S`.
the contents of the file is given below:-
```bash
muizz@LAPTOP-VF1FT9IQ:~$ cat chall_1.S.1
        .arch armv8-a
        .file   "chall_1.c"
        .text
        .align  2
        .global func
        .type   func, %function
func:
        sub     sp, sp, #32
        str     w0, [sp, 12]
        mov     w0, 85
        str     w0, [sp, 16]
        mov     w0, 6
        str     w0, [sp, 20]
        mov     w0, 3
        str     w0, [sp, 24]
        ldr     w0, [sp, 20]
        ldr     w1, [sp, 16]
        lsl     w0, w1, w0
        str     w0, [sp, 28]
        ldr     w1, [sp, 28]
        ldr     w0, [sp, 24]
        sdiv    w0, w1, w0
        str     w0, [sp, 28]
        ldr     w1, [sp, 28]
        ldr     w0, [sp, 12]
        sub     w0, w1, w0
        str     w0, [sp, 28]
        ldr     w0, [sp, 28]
        add     sp, sp, 32
        ret
        .size   func, .-func
        .section        .rodata
        .align  3
.LC0:
        .string "You win!"
        .align  3
.LC1:
        .string "You Lose :("
        .text
        .align  2
        .global main
        .type   main, %function
main:
        stp     x29, x30, [sp, -48]!
        add     x29, sp, 0
        str     w0, [x29, 28]
        str     x1, [x29, 16]
        ldr     x0, [x29, 16]
        add     x0, x0, 8
        ldr     x0, [x0]
        bl      atoi
        str     w0, [x29, 44]
        ldr     w0, [x29, 44]
        bl      func
        cmp     w0, 0
        bne     .L4
        adrp    x0, .LC0
        add     x0, x0, :lo12:.LC0
        bl      puts
        b       .L6
.L4:
        adrp    x0, .LC1
        add     x0, x0, :lo12:.LC1
        bl      puts
.L6:
        nop
        ldp     x29, x30, [sp], 48
        ret
        .size   main, .-main
        .ident  "GCC: (Ubuntu/Linaro 7.5.0-3ubuntu1~18.04) 7.5.0"
        .section        .note.GNU-stack,"",@progbits
muizz@LAPTOP-VF1FT9IQ:~$
```

In the function `func` initialization of variables happens.
`mov w0,85` assigns `w0` with `85` and then `str w0,[sp,16]` stores `w0` at or offset from `sp`.
`mov w0,6` assigns `w0` with `6` and then `str w0,[sp,20]` stores `w0` at or offset from `sp`.
`mov w0,3` assigns `w0` with `3` and then `str w0,[sp,24]` stores `w0` at or offset from `sp`.

[sp,16] --> 85,
[sp,20] --> 6,
[sp,24] --> 3.

`ldr     w0, [sp, 20]` means w0 = 6.
`ldr     w1, [sp, 16]` means w1 = 85.

`lsl     w0, w1, w0` performs logical left shift such that `w0 = w1 << w0` i.e. `w0 = 85 << 6` which comes out to be `w0 = 5440`.
`str     w0, [sp, 28]` stores `w0 = 5440` in `[sp,28]`.
`ldr     w1, [sp, 28]` loads `[sp,28]` in `w1` such that `w1 = 5440`.
`ldr     w0, [sp, 24]` loads0 `[sp,24]` in `w0` such that `w0 = 3`.
`sdiv    w0, w1, w0` performs division such that `w0 = w1 / w0` i.e. `w0 = 5440 / 3` which comes out to be `w0 = 1813` considering only integer value.
`str     w0, [sp, 28]` stores `w0 = 1813` at `[sp,28]`.
`ldr     w1, [sp, 28]` loads `[sp,28]` to `w1` such that `w1 = 1813`.
`ldr     w0, [sp, 12]` asssigns the argument to `w0`.
`sub     w0, w1, w0` performs subtraction such that `w0 = w1 - w0`.

in the `main` function we can see that `cmp     w0, 0` compares `w0`  with `0`. And if it is true it will print `win`.

Therfore, w0 should be equal to 1813, then only it will become zero.
1813 in hexadecimal =  00000715.

Flag: - `picoCTF{00000715}`

## References
1.) https://www.cs.princeton.edu/courses/archive/spr19/cos217/lectures/15_AssemblyFunctions.pdf
2.) https://modexp.wordpress.com/2018/10/30/arm64-assembly/#arithmetic
##
#
