# ARM Architecture

# Theory

 In this course, we dived into the kernel of ARM Cortex-M3 which have been widely applied in MCU by many vendors e.g. ST, TI. 

### Harvard Architecture

Different to the Von Neumann Model of PCs, Cortex-M family adopts the Harvard Arch. The most significant difference is the multi-bus system. In Harvard arch., there’re many buses e.g. I-bus, D-bus, System bus and PPB. Cortex-M3 adopt the AHB-Lite and APB protocols. So that the parallel instruction and data fetching is possible. Actually, this design hugely improve the speed of MCU. 

## Thumb-2 ISA

### Instruction

The ISA of Cortex-M3 is Thumb-2 which is evolved from Thumb. The former MCUs use the mixture of 16-bit Thumb and 32-bit ARM instr. Thumb-2 supports both 16-bit and 32-bit instructions so that it could juggle the code density and the performance, and avoid the overhead during switching the modes b/t ARM and Thumb mode.

### Registers

1. General Registers: General-Purpose registers, SP: Stack Pointer, LR: Link Register, 
PC: Program Counter
2. Special Registers
    1. xPSR: Program state register. APSR (Application), IPSR (Interrupt), EPSR (Exception)
    2. Mask registers: PRIMASK, FAULTMASK, BASEPRI
    3. Control Register

### Assembly

We also learned a few fundamental assembly language instruction: e.g. LDR/STR, MOV, ADD/SUB/MUL/…, PUSH/POP

## Memory System

This is a critical part in this course. Cortex-M3 has a memory address space of 4GB, and it’s divided to many sectors for different purpose. Beginning with the lowest one:

### Code

Code area is mainly used to store user’s program and the vector table. Commonly, Code area is read-only because it physically map to Flash/ROM. However, Cortex-M3 supports SRAM boot, in that case code area physically map to SRAM device. It become a kind of alias: code area and SRAM area map to the same physical memory. 

### SRAM

SRAM stores the stack and heap. The variables store in there. SRAM supports bit-band operation which means 1 word has 32 words of alias to implement atomic operation. Purpose: avoid R-M-W collision.

### Peripherals

The on-chip peripherals are controlled by modifying this area. E.g. GPIO, USART, I2C, TIM…. This area also support bit-band operation because we need to set 1 single bit to modify the pin status.

### External RAM

As the SRAM is not enough, this area is mapped to external memory.

### External Device

### SCS / Vendor preserved Area

The area is divided to 2 parts: 1. SCS (System Control Space), the SysTick, NVIC, SCB, MPU store here. 2. vendor preserved area: this area is preserved for vendors.

## Exception & Interrupt

The 2nd. critical part. 

### Types

Exception includes System exception and External Interrupt. Managed by NVIC and SCB in SCS. 

In Cortex-M3, There’re 255 exceptions: 
The top 15 are system exceptions and the rest 240 are interrupts.

### Priority

Processor arbitrate the exceptions with priority. The priorities of sys. exceptions are fixed and the priorities of interrupts are programmable with the priority-level register. The 8-bit register is divided to 2 parts: group priority (pre-empt priority) determining if the new interrupt preempt and sub-priority determining which one to service if there’re 2 interrupts with same group priority. The bits proportion defined by priority group. 

MCU has 3 registers to mask the exception: PRIMASK, FAULTMASK and BASEPRI.

### Vector table

The addresses of handlers are stored in vector table located in 0x0. If we want to modify the table, we need to relocate that with VTOR. VTOR is a pointer points to the beginning address of the vector table.

### NVIC

NVIC is the core managing interrupt. There’re a bunch of registers to control:

There’re 3 status of interrupts: Enable, Pending and Active. Correspondingly, there’re in NVIC: ISER, ICER, ISPR, ICPR, IABR. With these registers, we can modify or check the status of interrupts.

And there’s also registers for priority: IPR (IP). There’re 240 8-bit registers for up to 240 interrupts: IP[0]~IP[239]

STIR: Soft Triggered Interrupt Register. 

### Sequence

1. Entrance sequence
    
    As receiving the interrupt request, processor arbitrate the priority and it’s active: 
    Hardware automatically stack the registers: R0~R3, R12, LR, PC, xPSR.
    
2. Handling sequence
    
    Switch to Handler mode, call the ISR or exception handler.
    
3. Return sequence
    
    Meeting the “BX LR” instruction, processor will get into the return sequence: unstacking, and returning to the original PC.
    

1. Bus System/ Harvard Arch.
2. ISA: Thumb-2
3. Memory Address Space
4. NVIC