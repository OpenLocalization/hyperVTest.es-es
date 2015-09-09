***PLOC***ms.ContentId: C2593EA1-B182-4C71-8504-49691F619158
title: Step 1: Make sure your machine is compatible***PLOC***

#***PLOC***Step 1: Make sure your machine can run Hyper-V***PLOC***

***PLOC***Only Windows 10 Pro and Windows 10 Enterprise support Hyper-V.***PLOC***

> ***PLOC***If you're running Windows 10 Home -- you can upgrade to Win 10 Pro in the Activation page located in the security settings.***PLOC***
> ***PLOC***The "Go to store" link will take you to a page for upgrading.***PLOC***
> 

***PLOC***Hyper-V is not available in Windows 10 Mobile / Windows 10 Mobile Enterprise***PLOC***

***PLOC***Hyper-V requires at least 4 GB of RAM but you might need more if you want to run multiple virtual machines at the same time.***PLOC***

***PLOC***Starting in Windows 10, Hyper-V requires a 64-bit processor with Second Level Address Translation (SLAT).***PLOC***

##***PLOC***Verify hardware compatability***PLOC***

***PLOC***To verify compatability, open PowerShell or a Windows command prompt (cmd.exe) and type: ***PLOC***`systeminfo.exe`***PLOC***.***PLOC***
***PLOC***This will give you information about your computer.***PLOC***

***PLOC***All of the items under ***PLOC********PLOC***Hyper-V Requirements***PLOC********PLOC*** must have the value if ***PLOC********PLOC***Yes***PLOC********PLOC***.***PLOC***

!(media\systeminfo.png)

***PLOC***Relevant sections:***PLOC***

*   `OS Name`***PLOC*** -- Must be Windows 8 or higher and either Profession or Enterprise.***PLOC***
*   `Hyper-V Requirements`***PLOC*** -- all of these must be true (value of "Yes") but some can be configured in BIOS.***PLOC***
    
    *   `VM Monitor Mode Extensions`***PLOC*** -- Property of the hardware.***PLOC***
        ***PLOC***Hyper-V can not run on this machine.***PLOC***
    *   `Virtualization Enabled in Firmware`***PLOC*** -- Can be enabled in BIOS***PLOC***
    *   `Second Level Address Translation`***PLOC*** -- Property of the hardware.***PLOC***
        ***PLOC***Hyper-V can not run on this machine.***PLOC***
    *   `Data Execution Prevention Available`***PLOC*** -- Can be enabled in BIOS***PLOC***

***PLOC***If Hyper-V is already enabled, the Hyper-V Requirements section will read:  ***PLOC***


```
Hyper-V Requirements: A hypervisor has been detected. Features required for Hyper-V will not be displayed.

```


##***PLOC***Next Step:***PLOC***

[***PLOC***Step 2: Install Hyper-V***PLOC***](walkthrough_install.md)


