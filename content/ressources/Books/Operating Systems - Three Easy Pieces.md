---
title: Operating Systems - Three Easy Pieces
draft: false
publish: true
tags:
  - 📖
date: 2025-04-04
---
**Operating Systems: Three Easy Pieces**  
Remzi H. Arpaci-Dusseau and Andrea C. Arpaci-Dusseau  
Arpaci-Dusseau Books  
November, 2023 (Version 1.10)

[Source](https://pages.cs.wisc.edu/~remzi/OSTEP/)

## Introduction

2
There is a body of software, in fact, that is responsible for making it easy to run programs (even allowing you to seemingly run many at the same time), allowing programs to share memory, enabling programs to interact with devices, and other fun stuff like that. That body of software is called the **operating system** (OS) , as it is in charge of making sure the system operates correctly and efficiently in an easy-to-use manner. 
The primary way the OS does this is through a general technique that we call **virtualization**. That is, the OS takes a physical resource (such as the processor, or memory, or a disk) and transforms it into a more general, powerful, and easy-to-use virtual form of itself. Thus, we sometimes refer to the operating system as a virtual machine.

Because the OS provides these calls to run programs, access memory and devices, and other related actions, we also sometimes say that the OS provides a standard library to applications.

, the OS is sometimes known as a resource manager.

4
It turns out that the operating system, with some help from the hardware, is in charge of this illusion, i.e., the illusion that the system has a very large number of virtual CPUs. Turning a single CPU (or a small set of them) into a seemingly infinite number of CPUs and thus allowing many programs to seemingly run at once is what we call virtualizing the CPU, the focus of the first major part of this book.

6
Indeed, that is exactly what is happening here as the OS is virtualizing memory. Each process accesses its own private virtual address space (sometimes just called its address space), which the OS somehow maps onto the physical memory of the machine.

9
The third major theme of the course is persistence. In system memory, data can be easily lost, as devices such as DRAM store values in a volatile manner; when power goes away or the system crashes, any data in memory is lost. Thus, we need hardware and software to be able to store data persistently; such storage is thus critical to any system as users care a great deal about their data.

13
The key difference between a system call and a procedure call is that a system call transfers control (i.e., jumps) into the OS while simultaneously raising the hardware privilege level. User applications run in what is referred to as user mode which means the hardware restricts what applications can do; for example, an application running in user mode can’t typically initiate an I/O request to the disk, access any physical memory page, or send a packet on the network. When a system call is initiated (usually through a special hardware instruction called a trap), the hardware transfers control to a pre-specified trap handler (that the OS set up previously) and simultaneously raises the privilege level to kernel mode. In kernel mode, the OS has full access to the hardware of the system and thus can do things like initiate an I/O request or make more memory available to a program. When the OS is done servicing the request, it passes control back to the user via a special return-from-trap instruction, which reverts to user mode while simultaneously passing control back to where the application left off.

