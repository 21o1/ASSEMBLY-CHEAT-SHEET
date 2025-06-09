# Advanced Assembly Cheatsheet (NASM/YASM, x86/x64, System-Level)

This cheatsheet is designed for reverse engineers, OS developers, hypervisor researchers, and anyone diving deep into the lowest layers of x86/x64 CPU behavior.

## Virtual Memory and Paging

- `MOV CR3, EAX` - Set page directory base register (used in paging setup)
- `INVLPG [addr]` - Invalidate TLB entry for given virtual address
- `MOV CR0, EAX` - Enable paging by setting PG bit (bit 31) in CR0
- `MOV CR4, EAX` - Enables PAE (bit 5), enables SSE (bit 9, 10)
- `MOV EFER, RAX` - Extended Feature Enable Register (e.g., long mode)

## Hardware Breakpoints and Debug Registers

- `DR0–DR3` - Hold linear addresses for hardware breakpoints
- `DR6` - Status register, shows which breakpoint was triggered
- `DR7` - Control register for enabling/disabling breakpoints
- `MOV DRx, reg` - Set debug register values (requires ring 0 or hypervisor)

## SMM / VMX / Advanced Privilege Instructions

- `RSM` - Resume from System Management Mode
- `VMXON`, `VMXOFF`, `VMLAUNCH`, `VMRESUME` - Intel VMX virtualization instructions
- `VMCLEAR`, `VMPTRLD`, `VMPTRST` - Manage VM control structures
- `SGDT`, `SIDT`, `SLDT` - Store descriptor tables (GDT, IDT, LDT)
- `SWAPGS` - Swap GS base (used in syscall entry on x64)

## System Call Transitions (x64 Linux/Windows)

- `SYSCALL` - Fast system call for 64-bit user mode to kernel transition
- `SYSRET` - Return from fast syscall
- `INT 0x80` - Legacy system call for Linux (x86 only)
- `SYSENTER`, `SYSEXIT` - Fast call/return interface on Intel processors
- `MSR_*` - Read/write model-specific registers that control syscall/sysenter behavior

## Thread Local Storage & Segment Bases

- `GS` (Linux), `FS` (Windows) - Used for thread-local storage in 64-bit
- `MOV RAX, GS:[0x30]` - Access Windows TEB (Thread Environment Block)
- `MOV RAX, FS:[0x0]` - Access Linux thread pointer
- `ARCH_SET_FS/ARCH_SET_GS` - syscalls for setting FS/GS base

## Low-Level Boot / Bare-Metal

- `ORG 0x7C00` - Set origin for bootloader at 0x7C00
- `BITS 16 / BITS 32 / BITS 64` - Define instruction mode
- `JMP 0x0000:0x7C00` - Far jump to reset segment:offset in BIOS
- `INT 0x13`, `INT 0x10` - BIOS disk and video services (real mode)
- `CLI / STI / HLT` - Disable/enable interrupts, halt CPU

## Security Features / Mitigation Instructions

- `LFENCE`, `SFENCE`, `MFENCE` - Memory fences (used in Spectre/Meltdown mitigation)
- `RET POLINE`, `JMP POLINE` - Spectre-safe return/jump via indirect branch predictors
- `INTEL CET`: Shadow stack, indirect branch tracking (`ENDBR64`, `ENDBR32`)
- `WRGSBASE`, `RDGSBASE` - Direct access to FS/GS base in user mode (with FSGSBASE enabled)

## Vector Extensions (AVX512 / VEX / EVEX)

- `VADDPS`, `VMULPD`, `VGATHERDPD`, `VSUBPS` - Advanced SIMD instructions
- `ZMM0-ZMM31` - 512-bit AVX-512 registers
- `K0-K7` - Mask registers for AVX512 predication
- `EVEX prefix` - New encoding for AVX512 with masking and broadcasting
- `VZEROUPPER`, `VZEROALL` - Clear upper portions of YMM/ZMM registers to avoid performance penalties

