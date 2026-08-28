# Storage

#computer-fundamentals #hardware #storage #forensics

**Storage** refers to persistent hardware used to retain digital information beyond the lifetime of a running system. Operating systems, applications, configuration files, documents, databases, logs, and other data are stored persistently so that they remain available after shutdown or reboot. This distinguishes storage from [[RAM]], whose contents are normally lost when power is removed.

The two most common storage technologies in general-purpose computers are **Hard Disk Drives (HDDs)** and **Solid-State Drives (SSDs)**. HDDs store information magnetically on rotating platters and use mechanical read/write heads to access the data. SSDs use non-volatile flash memory and have no moving mechanical components. SSDs generally provide much lower access latency and substantially better random I/O performance than traditional HDDs.

Storage performance is not determined exclusively by its capacity. Important characteristics include **latency**, sequential throughput, random I/O performance, interface bandwidth, controller behaviour, queue depth, and the underlying storage technology. A storage device can therefore have a large capacity while still performing poorly for workloads dominated by random access.

SSDs introduce additional characteristics because flash memory cannot be overwritten indefinitely without management. SSD controllers use mechanisms such as wear levelling, garbage collection, and logical-to-physical address translation to distribute writes and maintain performance. The operating system and filesystem may also communicate information about blocks that are no longer required, allowing the storage device to optimise internal management.

Before applications can normally use persistent storage, it is organised into logical structures. A physical storage device may contain **partitions**, which can then contain filesystems. A filesystem provides abstractions for storing and organising files and directories, tracking metadata, managing free space, and controlling access. Examples include ext4 and other Linux filesystems, NTFS on Windows, and various filesystems used by other operating systems. See [[File-Systems]].

Storage is also closely connected to the operating system's boot process. A computer generally contains information required to locate and load an operating system, while the operating system subsequently mounts or otherwise accesses the relevant filesystems. The exact process depends on the platform, firmware configuration, partitioning scheme, bootloader, and operating system.

Persistent storage is particularly important from a cybersecurity perspective because it contains information that survives reboots and may remain accessible long after a user believes it has been deleted. Authentication databases, credentials, SSH keys, browser databases, application configuration, shell history, logs, malware samples, and system artefacts can all provide valuable information during security investigations.

Deleting a file does not necessarily mean that its underlying data immediately disappears from the physical medium. Filesystems generally remove references to data rather than instantly overwriting every associated storage location. On modern SSDs, internal controller behaviour and technologies such as garbage collection and wear levelling make physical data handling even more complex. Secure disposal must therefore consider the characteristics of the storage technology and the required security guarantees.

Storage can also contain **metadata** that is valuable during investigations. File timestamps, ownership information, permissions, directory structures, filesystem journals, application databases, and system logs can help reconstruct activity. Digital forensic investigations therefore frequently analyse storage at both the filesystem and lower levels.

Persistent storage also represents a major availability concern. Hardware failure, filesystem corruption, accidental deletion, ransomware, malicious modification, and insufficient capacity can all prevent systems or applications from functioning correctly. Security architecture consequently relies on mechanisms such as backups, redundancy, integrity verification, encryption, access control, and recovery procedures.

Storage encryption provides another important security control. **Full-disk encryption** or filesystem-level encryption can protect data from unauthorised access when the physical device is removed from its intended system or when a device is lost or stolen. Encryption does not eliminate the need for access control, however, because data may be available in plaintext while the operating system is running.

Understanding storage provides a foundation for studying [[File-Systems]], operating-system internals, disk and filesystem forensics, data recovery, secure deletion, encryption, incident response, and system resilience.