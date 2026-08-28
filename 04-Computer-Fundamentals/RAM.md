# RAM

#computer-fundamentals #hardware #memory

**Random Access Memory (RAM)** is the computer's primary volatile memory. It provides relatively fast temporary storage for the operating system, running applications, active processes, and the data they currently require. RAM is called volatile because its contents are normally lost when the system loses power.

RAM occupies an important position in the computer's **memory hierarchy**. [[CPU]] registers and processor caches provide faster access but have extremely limited capacity, while RAM provides substantially more capacity at higher latency. [[Storage]] provides persistent capacity that survives power loss, but it is significantly slower to access than RAM. Computer systems therefore move data between these layers according to current computational requirements.

When an application starts, the operating system loads the necessary executable code and data from [[Storage]] into RAM. While the application is running, the CPU can access this memory much more efficiently than persistent storage. Programs therefore operate primarily on memory-resident data, although they may continuously read from and write to storage as required.

RAM is not simply a single undifferentiated pool from the perspective of software. Modern operating systems implement **virtual memory**, giving each process its own virtual address space. Virtual addresses are translated into physical memory locations by mechanisms involving the CPU's Memory Management Unit (MMU) and operating-system memory management. This abstraction allows processes to operate independently while preventing ordinary applications from directly accessing memory belonging to other processes.

Virtual memory also allows the operating system to use more address space than the amount of immediately available physical RAM. When physical memory becomes constrained, systems may move less frequently used memory pages to persistent storage through mechanisms such as **swap** on Linux or a **page file** on Windows. This allows the system to continue operating under memory pressure, but storage access is considerably slower than physical RAM access.

RAM capacity therefore affects how much active data a system can maintain without relying heavily on storage-backed virtual memory. However, adding more RAM does not automatically make every workload faster. Performance depends on whether the workload is actually constrained by available memory, as well as on memory bandwidth, latency, CPU behaviour, and the characteristics of the applications being executed.

Different generations and types of RAM have different electrical and architectural characteristics. Modern systems commonly use **DRAM**, where each memory cell stores a bit of information using electrical charge that must periodically be refreshed. Desktop and laptop systems typically use standardised memory modules, while other devices may use memory technologies designed for lower power consumption or specialised performance requirements.

RAM also has an important security role because sensitive information may exist in memory while a system is running. Passwords, authentication tokens, encryption keys, browser sessions, application data, network information, and portions of files can all be present in RAM. Unlike persistent storage, memory contents can change rapidly as processes execute, making memory analysis particularly useful in digital forensics and incident response.

The operating system therefore applies memory isolation and access-control mechanisms to prevent processes from freely reading or modifying one another's memory. Hardware-assisted protections and techniques such as **Address Space Layout Randomization (ASLR)**, non-executable memory protections, and privilege separation further reduce the ability of malicious software to exploit memory in predictable ways.

RAM should therefore be understood not merely as "temporary storage", but as a critical execution environment connecting the [[CPU]] with running software. Understanding RAM provides a foundation for studying processes, virtual memory, memory corruption vulnerabilities, operating-system internals, and [[Digital-Forensics]].