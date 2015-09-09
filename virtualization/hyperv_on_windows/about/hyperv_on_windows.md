***PLOC***ms.ContentId: 93EDAAF5-E4FC-4F3F-AB55-669D2BF47D78
title: Introduction to Hyper-V on Windows 10***PLOC***

#***PLOC***Introduction to Hyper-V on Windows 10 test***PLOC***

***PLOC***Whether you are a software developer, an ITPro, or a tech enthusiast, many of you need to run multiple operating systems, occasionally on many different machines.***PLOC***
***PLOC***Not all of us have access to a full suite of labs to house all these machines, and so virtualization can be a space and time saver.***PLOC***

##***PLOC***Uses for virtualization***PLOC***

***PLOC***Virtualization enables anyone to easily maintain multiple test environments consisting of many operating systems, software configurations, and hardware configurations.***PLOC***
***PLOC***Hyper-V provides virtualization on Windows as well as a simple mechanism to quickly switch between these environments without incurring additional hardware costs.***PLOC***

***PLOC***Hyper-V can be used in many ways, for example:***PLOC***

*   ***PLOC***A test environment consisting of multiple virtual machines can be created on a single desktop or laptop computer.***PLOC***
    ***PLOC***Once testing has completed, these virtual machines can be exported and then imported into any other Hyper-V system.***PLOC***
*   ***PLOC***Developers can use Hyper-V on their computer to test software on multiple operating systems.***PLOC***
    ***PLOC***For example, if you have an application that must be tested on Windows 8, Windows 7 and a Linux operating system, multiple virtual machines can be created on your development system, one containing each of these operating systems.***PLOC***
*   ***PLOC***You can use Hyper-V to troubleshoot virtual machines from any Hyper-V deployment.***PLOC***
    ***PLOC***You can export a virtual machine from your production environment, open it on your desktop running Hyper-V, perform your required troubleshooting, and then export it back into the production environment.***PLOC***
*   ***PLOC***Using virtual networking, you can create a multi-machine environment for test/development/demonstration that is secure from affecting the production network.***PLOC***
*   ***PLOC***Enthusiasts can use it to experiment with other operating systems.***PLOC***
    ***PLOC***Hyper-V makes it very easy to bring up and tear down different operating systems.***PLOC***
*   ***PLOC***You can use Hyper-V on a laptop for demonstrating older versions of Windows or non-Windows operating systems.***PLOC***

##***PLOC***System requirements***PLOC***

***PLOC***Hyper-V requires a 64-bit system that has Second Level Address Translation (SLAT).***PLOC*** ***PLOC***SLAT is a feature present in the current generation of 64-bit processors by Intel & AMD.***PLOC*** ***PLOC***You’ll also need a 64-bit version of Windows 8 or greater, and at least 4GB of RAM.***PLOC*** ***PLOC***Hyper-V does support creation of both 32-bit and 64-bit operating systems in the VMs.***PLOC***

***PLOC***Hyper-V’s dynamic memory allows memory needed by the VM to be allocated and de-allocated dynamically (you specify a minimum and maximum) and share unused memory between VMs.***PLOC***
***PLOC***You can run 3 or 4 VMs on a machine that has 4GB of RAM but you'll need more RAM for 5 or more VMs.***PLOC***
***PLOC***On the other end of the spectrum, you can also create large VMs with 32 processors and 512GB RAM, depending on your physical hardware.***PLOC***

##***PLOC***Operating systems you can run in a virtual machine***PLOC***

***PLOC***The term "guest" refers to a virtual machine and "host" refers to the computer running the virtual machine.***PLOC***
***PLOC***Hyper-V on Windows supports many different guest operating systems including various releases of Linux, FreeBSD and Windows.***PLOC***
***PLOC***For information about which operating systems are supported as guests in Hyper-V on Windows, see ***PLOC***[***PLOC***Supported Windows Guest Operating Systems***PLOC***](supported_guest_os.md)***PLOC*** and ***PLOC***[***PLOC***Linux and FreeBSD Virtual Machines on Hyper-V***PLOC***](https://technet.microsoft.com/library/dn531030.aspx)***PLOC***.***PLOC***

##***PLOC***Differences between Hyper-V on Windows and Hyper-V on Windows Server***PLOC***

***PLOC***There are some features that work differently in Hyper-V on Windows than they do Hyper-V running on Windows Server.***PLOC***
***PLOC***These include the following:***PLOC***

*   ***PLOC***The memory management model is different for Hyper-V on Windows.***PLOC***
    ***PLOC***On a server, Hyper-V memory is managed with the assumption that only the virtual machines are running on the server.***PLOC***
    ***PLOC***In Hyper-V on Windows, memory is managed with the understanding most client machines are running software in addition to running virtual machines.***PLOC***
    ***PLOC***For example, a developer might be running Visual Studio as well as several virtual machines on the same computer.***PLOC***
*   ***PLOC***SR-IOV on a 64-bit guest works normally, but 32-bit does not and is not supported.***PLOC***

###***PLOC***Windows Server features not avilable in Windows Hyper-V***PLOC***

***PLOC***There are some features included in Hyper-V on server that are not included in Hyper-V on Windows.***PLOC***
***PLOC***These include the following:***PLOC***

*   ***PLOC***The Remote FX capability to virtualize GPUs ***PLOC***
*   ***PLOC***Live migration of virtual machines from one host to another***PLOC***
*   ***PLOC***Hyper-V Replica***PLOC***
*   ***PLOC***Virtual Fibre Channel***PLOC***
*   ***PLOC***SR-IOV networking***PLOC***
*   ***PLOC***Shared .VHDX***PLOC***

> *****PLOC***Warning***PLOC********PLOC***: Virtual machines running on Hyper-V do not automatically handle moving from a wired to a wireless connection.***PLOC***
> ***PLOC***You must change the virtual machines network adapter settings manually.***PLOC***
> 

##***PLOC***Limitations***PLOC***

***PLOC***Using virtualization does have limitations.***PLOC***
***PLOC***Features or applications that depend on specific hardware will not work well in a VM.***PLOC***
***PLOC***For example, games or applications that require processing with GPUs (without providing software fallback) might not work well.***PLOC***
***PLOC***Also, applications relying on sub 10ms timers, like latency-sensitive high-precision apps such as live music mixing apps, etc. could have issues running in a VM.***PLOC***
***PLOC***The root OS is also running on top of the Hyper-V virtualization layer, but it is special in that it has direct access to all the hardware.***PLOC***
***PLOC***This is why applications with special hardware requirements continue to work unhindered in the root OS but latency-sensitive, high-precision apps could still have issues running in the root OS.***PLOC***

***PLOC***As a reminder, you'll need to have a valid license for any operating systems you use in the VMs.***PLOC***

##***PLOC***Next step:***PLOC***

[***PLOC***Walkthrough Hyper-V on Windows 10***PLOC***](..\quick_start\walkthrough.md)

***PLOC***Check out ***PLOC***[***PLOC***What's New***PLOC***](whats_new.md)***PLOC*** in Hyper-V on Windows 10.***PLOC***


