# Windows

## Overview

Windows is a family of operating systems developed by Microsoft for personal computers, servers, and enterprise environments. It provides a graphical user interface (GUI), hardware abstraction, memory and process management, file systems, networking, and built-in security features. Windows is one of the most widely used operating systems and serves as the foundation for many corporate infrastructures.

---

## Windows Editions

Different Windows editions are designed for different use cases.

- **Home**: Intended for personal use with standard consumer features.
- **Pro**: Adds business-oriented capabilities such as BitLocker, Remote Desktop, and Group Policy support.
- **Enterprise**: Includes advanced security, virtualization, and centralized management features for organizations.
- **Education**: Similar to Enterprise but licensed for educational institutions.
- **Server**: Designed to provide enterprise services such as Active Directory, DNS, DHCP, file sharing, and virtualization.

---

## Graphical User Interface (GUI)

Windows primarily uses a graphical interface to interact with the operating system.

Common components include:

- **Desktop**: Main workspace where files, folders, and shortcuts are displayed.
- **Start Menu**: Central location for launching applications and accessing system settings.
- **Taskbar**: Displays running applications, pinned programs, and system controls.
- **Notification Area**: Contains system status icons such as network, audio, battery, and notifications.
- **File Explorer**: Used to browse, manage, and organize files and directories.

---

## File System

Modern Windows installations use **NTFS (New Technology File System)** as the default file system.

NTFS provides:

- File permissions
- Journaling
- Compression
- Encryption (EFS)
- Large file support
- Reliability and crash recovery

The operating system is typically installed in:

```text
C:\
```

Important directories include:

```text
C:\Windows
C:\Windows\System32
C:\Program Files
C:\Program Files (x86)
C:\Users
```

---

## User Accounts

Windows separates users through individual accounts and user profiles.

Two common account types exist:

- **Standard User**: Can use installed applications but has limited administrative privileges.
- **Administrator**: Has full control over the operating system, software installation, and system configuration.

Each user has a personal profile stored under:

```text
C:\Users\<username>
```

---

## User Account Control (UAC)

User Account Control (UAC) helps reduce the risk of unauthorized system changes by requiring administrative approval before privileged operations are executed.

Even when logged in as an administrator, applications run with standard privileges until elevated.

---

## Settings and Control Panel

Windows provides two configuration interfaces.

- **Settings** is the modern management application.
- **Control Panel** is the legacy interface that still contains many advanced configuration options.

Microsoft is gradually moving Control Panel functionality into Settings.

---

## Task Manager

Task Manager is a built-in monitoring and troubleshooting utility.

It allows administrators to:

- View running applications
- Monitor processes
- Analyze CPU, memory, disk, and network usage
- Manage startup applications
- End unresponsive tasks
- View logged-in users

---

## Administrative Tools

Windows includes numerous tools for system administration and troubleshooting.

### System Configuration (MSConfig)

Used to troubleshoot startup issues, configure boot options, and manage startup services.

### Computer Management

A centralized console that provides access to several administrative utilities.

It includes:

- Event Viewer
- Device Manager
- Disk Management
- Services
- Task Scheduler
- Shared Folders

### Device Manager

Displays installed hardware devices and their drivers.

### Event Viewer

Records system, security, and application logs used for troubleshooting and incident investigation.

### Disk Management

Creates, deletes, formats, resizes, and manages storage volumes.

### Services

Manages background services that run automatically or manually.

### Task Scheduler

Automates tasks by executing programs or scripts based on predefined triggers.

### Resource Monitor

Provides detailed real-time information about:

- CPU
- Memory
- Disk
- Network

### System Information (msinfo32)

Displays detailed information about:

- Hardware
- Drivers
- Installed components
- Software environment
- System configuration

### Registry Editor (regedit)

Allows administrators to view and modify the Windows Registry.

Improper changes may cause system instability or prevent Windows from booting correctly.

### Command Prompt

The traditional Windows command-line interpreter (`cmd.exe`) used for administration, troubleshooting, and automation.

---

## Windows Security

Windows includes multiple built-in security technologies that work together to protect the operating system.

### Windows Update

Installs:

- Security patches
- Bug fixes
- Driver updates
- Feature updates

Keeping Windows updated reduces exposure to known vulnerabilities.

### Windows Security

Windows Security centralizes several protection features, including:

- Virus & Threat Protection
- Firewall & Network Protection
- App & Browser Control
- Device Security
- Account Protection

### Microsoft Defender

Microsoft Defender is the built-in antivirus and anti-malware solution that provides real-time protection against malicious software.

### Windows Firewall

Filters inbound and outbound network traffic according to configured security rules, helping prevent unauthorized network access.

### BitLocker

BitLocker encrypts entire storage volumes to protect data if a device is lost or stolen.

It commonly integrates with the Trusted Platform Module (TPM) to securely store encryption keys.

### Volume Shadow Copy Service (VSS)

Volume Shadow Copy Service creates point-in-time snapshots of files and storage volumes.

These snapshots are used by backup software and Windows recovery features to restore previous versions of data.

## Command-Line Interfaces

Although Windows is primarily known for its graphical interface, it also provides powerful command-line environments for administration, troubleshooting, and automation.

Modern versions of Windows include two primary command-line interfaces:

- **Command Prompt (CMD)**, the traditional command interpreter.
- **PowerShell**, Microsoft's modern automation and scripting platform.

Many administrative tasks can be performed significantly faster through the command line than through graphical tools. System administrators, penetration testers, incident responders, and malware analysts frequently rely on command-line interfaces to inspect systems, gather information, automate repetitive tasks, and remotely manage Windows hosts.

## Windows Terminal

Windows Terminal is Microsoft's modern terminal application that provides a unified interface for multiple command-line environments.

Instead of replacing CMD or PowerShell, Windows Terminal acts as a host capable of running multiple shells simultaneously, including:

- Command Prompt (CMD)
- Windows PowerShell
- PowerShell
- Windows Subsystem for Linux (WSL)
- Azure Cloud Shell

It supports tabs, panes, customizable themes, Unicode, GPU-accelerated rendering, and extensive configuration options, making it the preferred terminal application on modern Windows systems.

## Environment Variables

Environment variables are system-defined or user-defined values that store configuration information used by Windows and applications.

They allow programs to locate important directories, determine system settings, and control application behavior.

Common environment variables include:

- `%PATH%`
- `%TEMP%`
- `%USERPROFILE%`
- `%SystemRoot%`
- `%ProgramFiles%`

Many Windows applications depend on these variables to locate executables and configuration files.

---

## Server Message Block (SMB)

**Server Message Block (SMB)** is a network protocol developed by Microsoft that enables systems to share files, printers, named pipes, and other resources across a network. It is widely used in Windows environments for file sharing, domain communication, and remote administration.

Modern Windows systems primarily use **SMBv2** and **SMBv3**, while **SMBv1** is deprecated due to multiple critical security vulnerabilities, including **MS17-010 (EternalBlue)**. SMB commonly operates over **TCP port 445**, with older implementations also relying on **NetBIOS over TCP/IP (port 139)**.

Because SMB often provides access to valuable resources and authentication services, it is one of the most frequently targeted protocols during penetration tests.

---

## NTLM Authentication

**NTLM (NT LAN Manager)** is Microsoft's legacy authentication protocol used to verify the identity of users without transmitting their passwords over the network. Instead of sending the password directly, NTLM uses a **challenge-response authentication** mechanism based on password hashes.

Although NTLM remains supported for backward compatibility, Microsoft recommends using **Kerberos** whenever possible because it provides stronger security and mutual authentication.

From an offensive security perspective, NTLM is commonly targeted through techniques such as **NTLM relay**, **Pass-the-Hash**, and **credential capture** attacks.

---

## Security Account Manager (SAM)

The **Security Account Manager (SAM)** is a Windows database that stores information about local user accounts, including password hashes and security identifiers (SIDs). The database is stored on disk and is protected by the operating system to prevent unauthorized access.

Attackers who obtain administrative or SYSTEM privileges may attempt to dump the contents of the SAM database to extract password hashes for offline cracking or Pass-the-Hash attacks.

The SAM only contains **local account credentials**. In Active Directory environments, domain account information is stored within the domain controller's **NTDS.dit** database instead.

---

## Protected View

**Protected View** is a Microsoft Office security feature that opens files originating from potentially untrusted sources in a restricted, read-only environment. Documents received through email, downloaded from the Internet, or obtained from other potentially unsafe locations are isolated to reduce the risk of malicious content executing automatically.

Its purpose is to protect users against malicious documents and phishing attacks by limiting active content until the user explicitly enables editing or other interactive features. Although it significantly improves security, vulnerabilities have occasionally allowed attackers to bypass Protected View protections.

---

## Windows Services

A **Windows Service** is a background process that runs independently of user interaction and performs system or application-related tasks. Services can start automatically during system boot, manually by an administrator, or when triggered by specific events.

Windows relies on services to provide essential functionality such as networking, printing, remote management, Windows Update, and security features. Administrators can manage services using the **Services** management console (`services.msc`), PowerShell, or the Command Prompt.

Misconfigured or vulnerable services are a common target during penetration tests because they may allow privilege escalation, persistence, or unauthorized code execution.

---

## Summary

Windows combines a graphical interface, robust file system, centralized administration tools, and layered security mechanisms to provide a flexible operating system for personal, business, and enterprise environments. Understanding these core components forms the foundation for Windows administration, troubleshooting, and security.