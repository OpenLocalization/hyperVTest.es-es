***PLOC***ms.ContentId: 7561B149-A147-4F71-9840-6AE149B9DED5
title: Supported Windows Guest Operating Systems***PLOC***

#***PLOC***Supported Windows guests***PLOC***

***PLOC***This article lists the Windows operating systems supported as guests in Hyper-V on Windows, as well provides information about integration services.***PLOC***

> ***PLOC***Windows 10 runs as a guest operating system on Windows 8.1 and Windows Server 2012 R2 Hyper-V hosts.***PLOC***
> 

##***PLOC***What does support mean?***PLOC***

***PLOC***Support means Microsoft has tested these host/guest combinations.***PLOC***
***PLOC***Issues with these combinations may receive attention from Product Support Services.***PLOC***

***PLOC***Microsoft provides support for guest operating systems in the following manner:***PLOC***

*   ***PLOC***Issues found in Microsoft operating systems and in integration services are supported by Microsoft support.***PLOC***
*   ***PLOC***For issues found in other operating systems that have been certified by the operating system vendor to run on Hyper-V, support is provided by the vendor.***PLOC***
*   ***PLOC***For issues found in other operating systems, Microsoft submits the issue to the multi-vendor support community, ***PLOC***[***PLOC***TSANet***PLOC***](http://www.tsanet.org/)***PLOC***.***PLOC***

##***PLOC***What are integration services and why do they matter?***PLOC***

***PLOC***Hyper-V includes integration services for supported guest operating systems.***PLOC***
***PLOC***Integration services improve interaction between the host system and the virtual machine.***PLOC***

***PLOC***Some operating systems (including different versions of Windows) have the integration services built-in, while others provide integration services through Windows Update.***PLOC***

##***PLOC***Supported Windows Server guest operating systems***PLOC***

***PLOC***For Windows 10 Hyper-V Hosts:***PLOC***

| ***PLOC***Guest operating system***PLOC***| ***PLOC***Maximum number of virtual processors***PLOC***| ***PLOC***Integration Services***PLOC***| ***PLOC***Notes***PLOC***| |
| -----                                | -----                                     | -----                     | -----     | ----- |
| ***PLOC***Windows Server Technical Preview***PLOC***| ***PLOC***64***PLOC***| ***PLOC***Built-in***PLOC***| | | |
| ***PLOC***Windows Server 2012 R2***PLOC***| ***PLOC***64***PLOC***| ***PLOC***Built-in***PLOC***| | | |
| ***PLOC***Windows Server 2012***PLOC***| ***PLOC***64***PLOC***| ***PLOC***Built-in***PLOC***| | | |
| ***PLOC***Windows Server 2008 R2 with Service Pack 1 (SP 1)***PLOC***| ***PLOC***64***PLOC***| ***PLOC***Install the integration services after you set up the operating system in the virtual machine.***PLOC***| ***PLOC***Datacenter, Enterprise, Standard and Web editions.***PLOC***| |
| ***PLOC***Windows Server 2008 with Service Pack 2 (SP 2)***PLOC***| ***PLOC***4***PLOC***| ***PLOC***Install the integration services after you set up the operating system in the virtual machine.***PLOC***| ***PLOC***Datacenter, Enterprise, Standard and Web editions (32-bit and 64-bit).***PLOC***| |
| ***PLOC***Windows Home Server 2011***PLOC***| ***PLOC***4***PLOC***| ***PLOC***Install the integration services after you set up the operating system in the virtual machine.***PLOC***| |
| ***PLOC***Windows Small Business Server 2011***PLOC***| ***PLOC***Essentials edition - 2, Standard edition - 4***PLOC***| ***PLOC***Install the integration services after you set up the operating system in the virtual machine.***PLOC***| ***PLOC***Essentials and Standard editions.***PLOC***| |

##***PLOC***Supported Windows guest operating systems***PLOC***

***PLOC***For Windows 10 Hyper-V Hosts:***PLOC***

| ***PLOC***Guest operating system***PLOC***| ***PLOC***Maximum number of virtual processors***PLOC***| ***PLOC***Integration Service***PLOC***| ***PLOC***Notes***PLOC***| |
| ----- | ----- | ----- | ----- | ----- |
| ***PLOC***Windows 10***PLOC***| ***PLOC***32***PLOC***| ***PLOC***Built-in***PLOC***| | |
| ***PLOC***Windows 8.1***PLOC***| ***PLOC***32***PLOC***| ***PLOC***Built-in***PLOC***| | |
| ***PLOC***Windows 8***PLOC***| ***PLOC***32***PLOC***| ***PLOC***Upgrade the integration services after you set up the operating system in the virtual machine.***PLOC***| | |
| ***PLOC***Windows 7 with Service Pack 1 (SP 1)***PLOC***| ***PLOC***4***PLOC***| ***PLOC***Upgrade the integration services after you set up the operating system in the virtual machine.***PLOC***| ***PLOC***Ultimate, Enterprise, and Professional editions (32-bit and 64-bit).***PLOC***| |
| ***PLOC***Windows 7***PLOC***| ***PLOC***4***PLOC***| ***PLOC***Upgrade the integration services after you set up the operating system in the virtual machine.***PLOC***| ***PLOC***Ultimate, Enterprise, and Professional editions (32-bit and 64-bit).***PLOC***| |
| ***PLOC***Windows Vista with Service Pack 2 (SP2)***PLOC***| ***PLOC***2***PLOC***| ***PLOC***Install the integration services after you set up the operating system in the virtual machine.***PLOC***| ***PLOC***Business, Enterprise, and Ultimate, including N and KN editions.***PLOC***| |
***PLOC*** Windows 10 is a guest operating system on Windows 8.1 and Windows Server 2012 R2 Hyper-V hosts.***PLOC***

##***PLOC***Linux and Free BSD***PLOC***

***PLOC***For Windows 10 Hyper-V Hosts:***PLOC***

| ***PLOC***Guest operating system***PLOC***| |
| -----|------|
| [***PLOC***CentOS and Red Hat Enterprise Linux ***PLOC***](https://technet.microsoft.com/library/dn531026.aspx)| |
| [***PLOC***Debian virtual machines on Hyper-V***PLOC***](https://technet.microsoft.com/library/dn614985.aspx)| |
| [***PLOC***SUSE***PLOC***](https://technet.microsoft.com/en-us/library/dn531027.aspx)| |
| [***PLOC***Oracle Linux***PLOC***](https://technet.microsoft.com/en-us/library/dn609828.aspx)| |
| [***PLOC***Ubuntu***PLOC***](https://technet.microsoft.com/en-us/library/dn531029.aspx)| |
| [***PLOC***FreeBSD***PLOC***](https://technet.microsoft.com/library/dn848318.aspx)| |
***PLOC***There are caveats around specific kernel versions.***PLOC***
***PLOC***For more information, including support information on past versions of Hyper-V, see ***PLOC***[***PLOC***Linux and FreeBSD Virtual Machines on Hyper-V***PLOC***](https://technet.microsoft.com/library/dn531030.aspx)***PLOC***.***PLOC***


