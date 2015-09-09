***PLOC***ms.ContentId: 34D5925A-D724-4552-9403-C2703A973234 
title: Migrating and upgrading virtual machines***PLOC***

#***PLOC***Migrate and upgrade virtual machines***PLOC***

***PLOC***If you move virtual machines to your Windows 10 host that were originally created with Hyper-V in Windows 8.1 or earlier, you won't be able to use the new virtual machine features until you manually update the virtual machine configuration version.***PLOC***

***PLOC***To upgrade the configuration version, shut down the virtual machine and then select to Upgrade Virtual Machine Configuration in Hyper-V Manager.***PLOC***
***PLOC***You can also open an elevated Windows PowerShell command prompt, and type:***PLOC***

***PLOC*** ```PowerShell
Update-VmVersion <vmname> | <vmobject>***PLOC***


```



## How do I check the configuration version of the virtual machines running on Hyper-V? 

To find the configuration version, open an elevated Windows PowerShell command prompt, and run the following command:

**Get-VM * | Format-Table Name, Version**

The PowerShell command produces the following sample output:


```

***PLOC***Name        State       CPUUsage(%) MemoryAssigned(M)   Uptime              Status                  Version***PLOC***

***PLOC***Atlantis    Running         0       1024                00:04:20.5910000    Operating normally      5.0***PLOC***

***PLOC***SGC VM      Running         0       538                 00:02:44.8350000    Operating normally      6.2
```***PLOC***

##***PLOC***What happens if I do not upgrade the configuration version?***PLOC***

***PLOC***If you have virtual machines that you created with an earlier version of Hyper-V, some features may not work with those virtual machines until you update the VM version.***PLOC***

***PLOC***Minimum VM configuration version for new Hyper-V features:***PLOC***

| *****PLOC***Feature Name***PLOC*****| *****PLOC***Minimum VM version***PLOC*****| |
| :------------------------------------- | -----------------: ||
| ***PLOC***Hot Add/Remove Memory***PLOC***| ***PLOC***6.0***PLOC***| |
| ***PLOC***Hot Add/Remove Network Adapters***PLOC***| ***PLOC***5.0***PLOC***| |
| ***PLOC***Secure Boot for Linux VMs***PLOC***| ***PLOC***6.0***PLOC***| |
| ***PLOC***Production Checkpoints***PLOC***| ***PLOC***6.0***PLOC***| |
| ***PLOC***PowerShell Direct***PLOC***| ***PLOC***6.2***PLOC***| |
| ***PLOC***Virtual Trusted Platform Module (vTPM)***PLOC***| ***PLOC***6.2***PLOC***| |
| ***PLOC***Virtual Machine Grouping***PLOC***| ***PLOC***6.2***PLOC***| |

##***PLOC***Virtual Machine Configuration Version***PLOC***

***PLOC***When you move or import a virtual machine to a host running Hyper-V on Windows 10 from host running Windows 8.1, the virtual machine’s configuration file isn't automatically upgraded.***PLOC***
***PLOC***This allows the virtual machine to be moved back to a host running Windows 8.1.***PLOC***
***PLOC***You won't have access to new virtual machine features until you manually update the virtual machine configuration version.***PLOC***

***PLOC***The virtual machine configuration version represents what version of Hyper-V the virtual machine’s configuration, saved state, and snapshot files it's compatible with.***PLOC***
***PLOC***Virtual machines with configuration version 5 are compatible with Windows 8.1 and can run on both Windows 8.1 and Windows 10.***PLOC***
***PLOC***Virtual machines with configuration version 6 are compatible with Windows 10 and won't run on Windows 8.1.***PLOC***

***PLOC***It is not necessary to upgrade all of your virtual machines simultaneously.***PLOC***
***PLOC***You can choose to upgrade specific virtual machines when required.***PLOC***
***PLOC***However, you won't have access to new the virtual machine features until you manually update the configuration version for each virtual machine.***PLOC***

----------------
**Important **

***PLOC***• After you upgrade the virtual machine configuration version, you can't move the virtual machine to a host that runs Windows 8.1.***PLOC***

***PLOC***• You can't downgrade the virtual machine configuration version from version 6 to version 5.***PLOC***

***PLOC***• You must turn off the virtual machine to upgrade the virtual machine configuration.***PLOC***

***PLOC***• After the upgrade, the virtual machine uses the new configuration file format.***PLOC***
***PLOC***For more information, see New virtual machine configuration file format.***PLOC***

--------

##***PLOC***What happens when I upgrade the version of a virtual machine?***PLOC***

***PLOC***When you manually upgrade the configuration version of a virtual machine to version 6.x, you'll change the file structure that is used for storing the virtual machines configuration and checkpoint files.***PLOC***

***PLOC***Upgraded virtual machines use a new configuration file format, which is designed to increase the efficiency of reading and writing virtual machine configuration data.***PLOC***
***PLOC***The upgrade also reduces the potential for data corruption in the event of a storage failure.***PLOC***

***PLOC***The following table lists the binary file locations and extension information for an upgraded virtual machine.***PLOC***

| *****PLOC***Virtual machine configuration and checkpoint files (version 6.x)***PLOC*****| *****PLOC***Description***PLOC*****| |
|:---------------|:----------------||
| *****PLOC***Virtual machine configuration***PLOC*****| ***PLOC***Configuration information is stored in a binary file format that uses the .vmcx extension.***PLOC***| |
| *****PLOC***Virtual machine Runtime State***PLOC*****| ***PLOC***Runtime state data is stored in a binary file format that uses the .vmrs extension.***PLOC***| |
| *****PLOC***Virtual machine virtual hard disk***PLOC*****| ***PLOC***The virtual hard disk files for the virtual machine.***PLOC******PLOC***They use .vhd or .vhdx file extensions.***PLOC***| |
| *****PLOC***Automatic  virtual hard disk files***PLOC*****| ***PLOC***The differencing disk files used for virtual machine checkpoints.***PLOC******PLOC***They use the .avhdx file extensions.***PLOC***| |
| *****PLOC***Checkpoint Files***PLOC*****| ***PLOC***Checkpoints are stored in multiple checkpoint files.***PLOC******PLOC***Each checkpoint creates a configuration file and runtime state file.***PLOC******PLOC***Checkpoint files use the .vmrs and .vmcx file extensions.***PLOC******PLOC***These new file formats are also used for production checkpoints and standard checkpoints.***PLOC***| |
***PLOC***After you upgrade the virtual machine configuration version to version 6.x, it is not possible to downgrade from version 6.x to version 5.***PLOC***

***PLOC***The virtual machine must be turned off to upgrade the virtual machine configuration.***PLOC***

***PLOC***The following table lists the default file locations for new or upgraded virtual machines.***PLOC***

| *****PLOC***Virtual Machine Files (Version 6.x)***PLOC*****| *****PLOC***Description***PLOC*****| |
|:-----|:-----||
| *****PLOC***Virtual machine configuration file***PLOC*****| ***PLOC***C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Machines***PLOC***| |
| *****PLOC***Virtual machine runtime state file***PLOC*****| ***PLOC***C:\ProgramData\Microsoft\Windows\Hyper-V\Virtual Machines***PLOC***| |
| *****PLOC***Checkpoint Files (.vmrs, .vmcx)***PLOC*****| ***PLOC***C:\ProgramData\Microsoft\Windows\Snapshots***PLOC***| |
| *****PLOC***Virtual hard disk file (.vhd/.vhdx)***PLOC*****| ***PLOC***C:\Users\Public\Documents\Hyper-V\Virtual Hard Disks***PLOC***| |
| *****PLOC***Automatic virtual hard disk files (.avhdx)***PLOC*****| ***PLOC***C:\Users\Public\Documents\Hyper-V\Virtual Hard Disks***PLOC***| |


