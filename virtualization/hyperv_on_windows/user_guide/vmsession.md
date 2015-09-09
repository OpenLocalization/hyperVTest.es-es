***PLOC***ms.ContentId: e586a11a-870f-403b-8af8-4c2931589d26
title: Manage Windows with PowerShell Direct ***PLOC***

#***PLOC***Manage Windows with PowerShell Direct***PLOC***

***PLOC***You can use PowerShell Direct to remotely manage a Windows 10 or Windows Server Technical Preview virtual machine from a Windows 10 or Windows Server Technical Preview Hyper-V host.***PLOC***
***PLOC***PowerShell Direct allows PowerShell management inside a virtual machine regardless of the network configuration or remote management settings on either the Hyper-V host or the virtual machine.***PLOC***
***PLOC***This makes it easier for Hyper-V Administrators to automate and script virtual machine management and configuration.***PLOC***

***PLOC***There are two ways to run PowerShell Direct:  ***PLOC***

*   ***PLOC***Create and exit a PowerShell Direct session using PSSession cmdlets***PLOC***
*   ***PLOC***Run script or command with the Invoke-Command cmdlet***PLOC***

***PLOC***If you're managing older virtual machines, use Virtual Machine Connection (VMConnect) or ***PLOC***[***PLOC***configure a virtual network for the virtual machine***PLOC***](http://technet.microsoft.com/library/cc816585.aspx)***PLOC***.***PLOC***

##***PLOC***Create and exit a PowerShell Direct session using PSSession cmdlets***PLOC***

1.  ***PLOC***On the Hyper-V host, open Windows PowerShell as Administrator.***PLOC***
2.  ***PLOC***Run the one of the following commands to create a session by using the virtual machine name or GUID:  
    ``` PowerShell
    Enter-PSSession -VMName <VMName>
    Enter-PSSession -VMGUID <VMGUID>***PLOC***


```

4. Run whatever commands you need to. These commands run on the virtual machine that you created the session with.
5. When you're done, run the following command to close the session:  
``` PowerShell
Exit-PSSession 

```


> ***PLOC***Note:  If you're session won't connect, make sure you're using credentials for the virtual machine you're connecting to -- not the Hyper-V host.***PLOC***
> 

***PLOC***To learn more about these cmdlets, see ***PLOC***[***PLOC***Enter-PSSession***PLOC***](http://technet.microsoft.com/library/hh849707.aspx)***PLOC*** and ***PLOC***[***PLOC***Exit-PSSession***PLOC***](http://technet.microsoft.com/library/hh849743.aspx)***PLOC***.***PLOC***

##***PLOC***Run script or command with Invoke-Command cmdlet***PLOC***

***PLOC***You can use the ***PLOC***[***PLOC***Invoke-Command***PLOC***](http://technet.microsoft.com/library/hh849719.aspx)***PLOC*** cmdlet to run a pre-determined set of commands on the virtual machine.***PLOC***
***PLOC***Here is an example of how you can use the Invoke-Command cmdlet where PSTest is the virtual machine name and the script to run (foo.ps1) is in the script folder on the C:/ drive:***PLOC***

***PLOC*** ``` PowerShell
 Invoke-Command -VMName PSTest -FilePath C:\script\foo.ps1 ***PLOC***


 ```

To run a single command, use the **-ScriptBlock** parameter:

 ``` PowerShell
 Invoke-Command -VMName PSTest -ScriptBlock { cmdlet } 

 ```


##***PLOC***What's required to use PowerShell Direct?***PLOC***

***PLOC***To create a PowerShell Direct session on a virtual machine,***PLOC***

*   ***PLOC***The virtual machine must be running locally on the host and booted.***PLOC***
*   ***PLOC***You must be logged into the host computer as a Hyper-V administrator.***PLOC***
*   ***PLOC***You must supply valid user credentials for the virtual machine.***PLOC***
*   ***PLOC***The host operating system must run Windows 10, Windows Server Technical Preview, or a higher version.***PLOC***
*   ***PLOC***The virtual machine must run Windows 10, Windows Server Technical Preview, or a higher version.***PLOC***

***PLOC***You can use the ***PLOC***[***PLOC***Get-VM***PLOC***](http://technet.microsoft.com/library/hh848479.aspx)***PLOC*** cmdlet to check that the credentials you're using have the Hyper-V administrator role and to see which VMs are running locally on the host and booted.***PLOC***

##***PLOC***What can you do with PowerShell Direct?***PLOC***

***PLOC***See ***PLOC***[***PLOC***PowerShell Direct snippets***PLOC***](../develop/powershell_snippets.md)***PLOC*** for numerous examples of how to use PowerShell Direct in your environment as well as tips and tricks for writing Hyper-V scripts with PowerShell.***PLOC***


