***PLOC***ms.ContentId: D1D4969F-52FD-43A2-982B-B531B0343D2B 
title: Troubleshooting***PLOC***

#***PLOC***Troubleshoot Hyper-V on Windows 10***PLOC***

##***PLOC***I updated to Windows 10 and now I can't connect to my downlevel (Windows 8.1 or Server 2012 R2) host***PLOC***

***PLOC***In Windows 10, Hyper-V manager moved to WinRM for remote management.***PLOC***
***PLOC***What that means is now Remote Management has to be enabled on the remote host in order to use Hyper-V manager to manage it.***PLOC***

***PLOC***For more information see ***PLOC***[***PLOC***Managing Remote Hyper-V Hosts***PLOC***](remote_host_management.md)

##***PLOC***I changed the checkpoint type, but it is still taking the wrong type of checkpoint***PLOC***

***PLOC***If you are taking the checkpoint from VMConnect and you change the checkpoint type in Hyper-V manager the checkpoint taken be whatever checkpoint type was specified when VMConnect was opened.***PLOC***

***PLOC***Close VMConnect and reopen it to make it take the correct type of checkpoint.***PLOC***

##***PLOC***When I try to create a virtual hard disk on a flash drive, an error message is displayed***PLOC***

***PLOC***Hyper-V does not support FAT/FAT32 formatted disk drives since these file systems do not provide access control lists (ACLs) and do not support files larger than 4GB.***PLOC***
***PLOC***ExFAT formatted disks only provide limited ACL functionality and are therefore also not supported for security reasons.***PLOC***
***PLOC***The error message displayed in PowerShell is "The system failed to create '\[path to VHD\]': The requested operation could not be completed due to a file system limitation (0x80070299)."***PLOC***

***PLOC***Use a NTFS formatted drive instead.***PLOC***

##***PLOC***I get this message when I try to install: "Hyper-V cannot be installed: The processor does not support second level address translation (SLAT)."***PLOC***

***PLOC***Hyper-V requires SLAT in order to run virtual machines.***PLOC***
***PLOC***If you computer does not support SLAT, then it cannot be a host for virtual mahchines.***PLOC***

***PLOC***If you are only trying to install the management tools, unselect ***PLOC********PLOC***Hyper-V Platform***PLOC********PLOC*** in ***PLOC********PLOC***Programs and Features***PLOC********PLOC*** > ***PLOC********PLOC***Turn Windows features on or off***PLOC********PLOC***.***PLOC***


