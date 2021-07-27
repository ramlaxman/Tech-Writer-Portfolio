# Memory Mapping in Linux operating system

Definitions
    
High Memory: Memory for which logical addresses do not exist because it is beyond address range set aside for kernel virtual addresses.
Low Memory: Memory for which logical addresses exist in kernel space. On almost every system you’ll likely encounter, all memory is low memory.

Memory mapped to Kernel

High Memory: Memory mapped to address space of the kernel.
Low Memory: No direct kernel mapping


Usage

Kernel itself (active modules i.e. checkpoint kernel modules) use low memory

User processes (except kernel processes) use both high and low memory.


On x86 arch or 32 bits systems, ratio of memory allocation is as follows: 

Kernel : user = 1 : 3 for 4 GB of Primary memory.


