---
title: "What happens when you power on a computer?"
categories:
  - Tech
tags:
  - OperatingSystem
toc: true
---
I am developing two operating systems in parallel – Test2OS and PLPOS. Both are toy OS. Test2OS is targeted for x86 architecture where as PLPOS is targeted for PLP architecture, a MIPS based architecture. The main purpose of Test2OS is just to learn operating system. I would like to implement all the basic concepts of Operating System in Test2OS. So based on that knowledge, PLPOS will be developed. Test2OS is already started and its code will be mostly from different kernel development tutorials website and PLPOS development will start soon. So as I learn and develop, I would like to present these concepts in different blog posts. Okay let’s get back to this one.
{: style="text-align: justify;"}

It’s a simple question “What really happens moment you press the power button in a computer?”. Well you may say our Operating System (Windows/Ubuntu like) will start. Yes true but how does that start? How does your processor, say Intel i7 knows that Windows operating system is installed in your hard disk and it has to start running it?
Before our operating system starts running, there is 2 crucial steps – BIOS and Bootloader. After these two steps comes our operating system. BIOS will load the Bootloader and Bootloader intern loads the kernel or operating system.
{: style="text-align: justify;"}

This post is all about BIOS – Basic Input Output System. BIOS gives the first set of instructions to be executed by the CPU. As this is the first thing to be run, it cannot reside on a volatile memory like RAM. Earlier systems used hold BIOS in ROM nowadays it is in Flash memory. All the setting related to BIOS are stored in a CMOS chip. Also all the address referred by BIOS is predefined. So when the power on button of the system is pressed, a signal will be sent to mother board. If computer is connected to an active power supply, mother board will send that signal to Power Supply Unit. Power Supply Unit will start providing power supply to various hardware. Once PSU is satisfied that sufficient power is available to each of the hardware/devices, it will send a Power_Good signal to the BIOS. Now BIOS will start its work.
{: style="text-align: justify;"}

BIOS main work is to find the bootable device. Apart from this main task, it has certain subtasks
1. Do a hardware test – Check if all the hardware or devices are working fine.
2. Initializing different registers
3. Activate BIOS of other devices like graphical processor
4. Create interrupt vector table
5. Manage some settings related to Hard disk, clocks, etc.

So BIOS has received Power_Good. Now first thing it will do is hardware test. Power on Self Test (POST). Some of the tests done are RAM read and write, keyboard test, etc. POST will be skipped if system is doing a warm boot. If 0x123h value is present at address 0000:04772 then it has to do warm boot, else it has to do cold boot. Usually when you are powering on after shutdown that will result in cold boot. If you are just restarting the machine then it will result in warm boot. Once this is done and verified all are working fine, it will create the interrupt vector table so that we can talk to different hardware devices using the interrupts mentioned in this table. In the earlier Operating Systems,  OS will use the interrupts given by BIOS and BIOS will do the talking with hardware but nowadays it is done directly by the OS. Next work of BIOS is to initialize all the registers like AX, BX, DS, CS, etc. Usually everything will be set to 0. BIOS program is always located in a reserved memory area – upper 64K of the first megabyte of system memory. BIOS ROM address will be 0xFFFF0h. So the code segment register is initialized with selector 0xF000h, base register with value 0xFFFF0000h and limit register as 0xFFFFh. Effectively this address is 4GB – 16 bytes = 0xFFFFFFF0h. This is mapped to System ROM mirroring address 0x000FFFF0h. Okay this is very confusing and I know it is and this is best I could come up with to explain. I guess I have quoted directly from one of the reference.
{: style="text-align: justify;"}

Next it will check its CMOS chip to see if there are any other BIOS in the system like BIOS of graphical processor unit. It will run those BIOS one by one. Once all these things are done, it will raise the int 0x19h  interrupt. The BIOS would have created interrupt vector table in RAM from 0 to 0x400h address. The address 0x401 to 0x500 is reserved for the BIOS itself. The work of interrupt 0x19 is to locate the bootable device. Again in CMOS setting, we would have set an order for checking the bootable device  like first hard disk, then cdrom and finally floppy disk. As soon as it finds a bootable device it will stop the search. Thats why order is important. Suppose you have two bootable device Hard disk and CD-ROM, boot order is CD-ROM and Hard disk, then it will always run from CD-ROM and never reach Hard disk.
{: style="text-align: justify;"}

BIOS does not care for the content of the bootable device. It will first check whether it is able to read the first chunk (512 byte – 1st sector) from the bootable device. If so then it will copy that chunk to RAM at address 0x0000:0x7C00.  Sometimes it will check for boot signature that is if 511st and 512nd byte values are 0x55 and 0xAA. Once copied and verified boot signature, BIOS will jump to the address 0x000:0x7C00 to start the booting of the Operating System.
When you power on the system, you wont realize that BIOS is doing this much work in the background. Everything happens so fast.  Now that we have identified our bootable device and loaded bootloader code to RAM, next post will be related to booting of Operating System till then read the references of this post.
{: style="text-align: justify;"}

Let me again put it. I am still learning and I may do a lot of mistakes in this post. If mistakes are there, then point it out so that I can learn and correct it. If its good then put a comment, like it or share it.
{: style="text-align: justify;"}

References:
Many of the content I read it from the following links. Some of them what I have written might have come directly from these articles.
* [http://computer.howstuffworks.com/bios1.htm](http://computer.howstuffworks.com/bios1.htm)
* [http://www.pcguide.com/ref/mbsys/bios/index.htm](http://www.pcguide.com/ref/mbsys/bios/index.htm)
* [https://en.wikipedia.org/wiki/BIOS](https://en.wikipedia.org/wiki/BIOS)
* [http://www.brokenthorn.com/Resources/OSDev3.html](http://www.brokenthorn.com/Resources/OSDev3.html)