# Advanced Assembly Language Cheatsheet (NASM/YASM)

This cheatsheet covers a broad set of NASM/YASM-compatible x86 and x86_64 assembly language instructions and directives.

## Data Definition & Directives

- `db - Define byte`
- `dw - Define word (2 bytes)`
- `dd - Define double word (4 bytes)`
- `dq - Define quad word (8 bytes)`
- `resb - Reserve byte(s)`
- `resw - Reserve word(s)`
- `resd - Reserve dword(s)`
- `section .data - Initialized data section`
- `section .bss - Uninitialized data section`
- `section .text - Code section`
- `global _start - Make _start symbol visible to linker`

## Registers (x86/x64)

- `General Purpose: eax, ebx, ecx, edx, esi, edi, esp, ebp (x86)`
- `64-bit: rax, rbx, rcx, rdx, rsi, rdi, rsp, rbp, r8–r15`
- `Segment Registers: cs, ds, es, fs, gs, ss`
- `Flags Register: eflags/rflags`

## Arithmetic & Logic Instructions

- `add, sub, mul, imul, div, idiv`
- `inc, dec, neg`
- `and, or, xor, not`
- `shl, shr, sal, sar, rol, ror`
- `cmp - Compare`
- `test - Bitwise AND, sets flags`

## Control Flow

- `jmp - Unconditional jump`
- `je/jz - Jump if equal/zero`
- `jne/jnz - Jump if not equal/non-zero`
- `jg/jnle, jl/jnge, jge/jnl, jle/jng - Signed jumps`
- `ja/jnbe, jb/jnae, jae/jnb, jbe/jna - Unsigned jumps`
- `loop, loope, loopne - Loop based on ecx/rcx and flags`
- `call - Call procedure`
- `ret - Return from procedure`
- `int - Software interrupt`

## Stack Operations

- `push, pop`
- `pusha/pushad, popa/popad - Push/pop all general registers (x86)`
- `pushf, popf - Push/pop flags`

## Memory Access

- `mov - Move data`
- `movsx, movzx - Sign/zero extend`
- `lea - Load effective address`
- `stosb/stosd, lodsb/lodsd, movsb/movsd - String ops`
- `rep movsb, rep stosb - Repeat string operation`

## System Calls (Linux x86_64)

- `mov rax, syscall_number`
- `mov rdi, arg1`
- `mov rsi, arg2`
- `mov rdx, arg3`
- `syscall`

## Bit Manipulation

- `bsf, bsr - Bit scan forward/reverse`
- `bt, bts, btr, btc - Bit test/set/reset/complement`

## Advanced Instructions

- `cpuid - Processor information`
- `rdtsc - Read time-stamp counter`
- `rdmsr/wrmsr - Read/write MSR`
- `in, out - Port I/O`
- `hlt - Halt processor`
- `nop - No operation`

## Privileged & Debug

- `cli, sti - Clear/set interrupt flag`
- `int 3 - Debug breakpoint`
- `iret - Interrupt return`
- `lgdt, sgdt, lidt, sidt - Descriptor tables`
- `ltr, str - Load/store task register`

## SIMD / FPU / MMX / AVX Basics

- `movq, movdqa, paddq, pmuludq - SSE/AVX integer operations`
- `addss, mulss, subss - Single-precision float`
- `addsd, mulsd, subsd - Double-precision float`
- `fld, fstp - FPU load/store`
- `fxch, fadd, fmul - FPU stack ops`

## Sample Directives (NASM)

- `%define, %macro, %if, %include, %assign, %strcat`
- `%rep, %endrep - Loop macros`
- `%error, %warning - Compilation feedback`

