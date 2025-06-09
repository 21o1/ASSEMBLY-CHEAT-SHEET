# Advanced Assembly Language Cheatsheet (NASM/YASM)

This extended cheatsheet is aimed at advanced users who work with x86/x86_64 assembly using NASM or YASM syntax.

## Data Definition & Directives

- `db` - Define byte (8-bit). Example: `db 0x1F`
- `dw` - Define word (16-bit). Example: `dw 0x1234`
- `dd` - Define double word (32-bit). Example: `dd 0x12345678`
- `dq` - Define quad word (64-bit). Example: `dq 0x123456789ABCDEF0`
- `resb`, `resw`, `resd`, `resq` - Reserve uninitialized storage. Useful in `.bss` section.
- `section .data` - Used for initialized data
- `section .bss` - Used for uninitialized data
- `section .text` - Used for code segment
- `global` - Makes symbol accessible to linker or other object files. Example: `global _start`
- `extern` - Declares external symbol from another file

## Registers (x86/x64)

- `EAX, EBX, ECX, EDX` - General purpose registers (32-bit)
- `RAX, RBX, RCX, RDX, R8-R15` - Extended registers (64-bit)
- `AX, AL, AH` - Lower parts of EAX (16, 8, 8-bit)
- `ESP, EBP, RSP, RBP` - Stack pointers (32/64-bit)
- `Segment Registers: CS, DS, SS, ES, FS, GS` - Used for segmented memory model
- `EFLAGS/RFLAGS` - Status and control flags. Includes ZF (zero), CF (carry), SF (sign), OF (overflow)

## Arithmetic & Logic Instructions

- `ADD dest, src` - Add `src` to `dest`
- `SUB dest, src` - Subtract `src` from `dest`
- `MUL reg/mem` - Unsigned multiply (result in AX, DX:AX)
- `IMUL` - Signed multiplication, supports 3-operand form
- `DIV`, `IDIV` - Unsigned/signed division (quotient in AL or AX, remainder in AH or DX)
- `INC`, `DEC` - Increment/decrement by 1
- `NEG` - Negate (two's complement)
- `AND`, `OR`, `XOR`, `NOT` - Bitwise logical operations
- `SHL`, `SHR` - Logical shift left/right
- `SAL`, `SAR` - Arithmetic shift left/right (preserves sign)
- `ROL`, `ROR` - Rotate bits left/right

## Control Flow

- `JMP label` - Unconditional jump to label
- `JE`, `JZ` - Jump if equal / zero flag set
- `JNE`, `JNZ` - Jump if not equal / zero flag clear
- `JG`, `JL`, `JGE`, `JLE` - Signed comparisons
- `JA`, `JB`, `JAE`, `JBE` - Unsigned comparisons
- `CALL` - Call a procedure (pushes return address)
- `RET` - Return from procedure
- `INT n` - Software interrupt, e.g., `INT 0x80` (Linux syscall, 32-bit)
- `LOOP`, `LOOPE`, `LOOPNE` - Loop with ECX/RCX countdown

## Memory Access

- `MOV dest, src` - Copy data between registers/memory/immediates
- `MOVZX`, `MOVSX` - Move with zero/sign extension
- `LEA reg, [mem]` - Load Effective Address; compute address without accessing memory
- `REP MOVSB`, `REP STOSB` - Repeat string operation based on ECX/RCX count
- `LODS`, `STOS` - Load/store string operation from AL/AX/EAX/RAX

## Stack Operations

- `PUSH reg/imm` - Push value onto stack (decrements ESP/RSP)
- `POP reg` - Pop value from stack (increments ESP/RSP)
- `PUSHA`, `POPA` - Push/pop all general registers (x86 only)
- `PUSHF`, `POPF` - Push/pop EFLAGS/RFLAGS

## System Calls (Linux x86_64)

- Syscall interface: use `MOV` to set syscall number and arguments
- `MOV RAX, syscall_number`
- `MOV RDI, arg1`, `MOV RSI, arg2`, `MOV RDX, arg3` etc.
- `SYSCALL` - Executes the system call (replaces `INT 0x80` in x86_64)
- Example (write): `MOV RAX, 1`, `MOV RDI, 1`, `MOV RSI, msg`, `MOV RDX, len`, `SYSCALL`

## Bit Manipulation

- `BT reg, bit` - Bit test
- `BTS`, `BTR`, `BTC` - Bit test and set/reset/complement
- `BSF`, `BSR` - Bit scan forward/reverse (find first/last set bit)

## Advanced Instructions

- `CPUID` - Query CPU features
- `RDTSC` - Read timestamp counter (for timing)
- `IN`, `OUT` - Port I/O (used in drivers/firmware)
- `NOP` - No operation
- `HLT` - Halt CPU until next interrupt
- `WAIT`, `FWAIT` - Wait for FPU to complete

## Privileged & Debug

- `CLI`, `STI` - Clear/set interrupt flag
- `IRET` - Return from interrupt
- `INT3` - Debug breakpoint
- `LGDT`, `SGDT`, `LIDT`, `SIDT` - Load/store descriptor tables
- `LTR`, `STR` - Load/store task register

## SIMD / MMX / SSE / AVX

- `MOVDQA`, `MOVAPS`, `MOVDQU` - Load/store aligned/unaligned 128-bit values
- `PADD`, `PMUL` - Packed add/multiply for integers
- `ADDSS`, `SUBSS`, `MULSS` - Scalar single precision float
- `ADDSD`, `SUBSD`, `MULSD` - Scalar double precision float
- `FADD`, `FMUL`, `FSUB` - FPU operations on FPU stack
- `FXCH` - Exchange FPU stack values

## NASM Preprocessor Directives

- `%define name value` - Constant definition
- `%macro name n` - Define macro with n arguments
- `%if`, `%else`, `%endif` - Conditional compilation
- `%include` - Include another file
- `%assign`, `%strlen`, `%substr`, `%strcat` - String operations
- `%rep`, `%endrep` - Repeat block

