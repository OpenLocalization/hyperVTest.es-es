***PLOC***ms.ContentId: B9414110-BEFD-423F-9AD8-AFD5EE612CDA
title: Step 8: Experiment with Windows PowerShell***PLOC***

#***PLOC***Step 8: Experiment with Windows PowerShell***PLOC***

***PLOC***Now that you have walked through the basics of deploying Hyper-V, creating virtual machines and managing these virtual machines, let’s explore how you can automate many of these activities with PowerShell.***PLOC***

###***PLOC***Return a list of Hyper-V commands***PLOC***

1.  ***PLOC***Click on the Windows start button, type ***PLOC********PLOC***PowerShell***PLOC********PLOC***.***PLOC***
2.  ***PLOC***Run the following command to display a searchable list of PowerShell commands available with the Hyper-V PowerShell Module.***PLOC***
    
    ***PLOC***```powershell
    get-command –module hyper-v | out-gridview***PLOC***


```
  You get something like this:

  ![](media\command_grid.png)

3. To learn more about a particular PowerShell command use `get-help`. For instance running the following command will return information about the `get-vm` Hyper-V command.

  ```powershell
get-help get-vm

```

***PLOC*** The output shows you how to structure the command, what the required and optional parameters are, and the aliases that you can use.***PLOC***

!(media\get_help.png)

###***PLOC***Return a list of virtual machines***PLOC***

***PLOC***Use the ***PLOC***`get-vm`***PLOC*** command to return a list of virtual machines.***PLOC***

1.  ***PLOC***In PowerShell, run the following command:***PLOC***
    
    `powershell
    get-vm
    `***PLOC***
    This displays something like this:***PLOC***
    
    !(media\get_vm.png)
2.  ***PLOC***To return a list of only powered on virtual machines add a filter to the ***PLOC***`get-vm`***PLOC*** command.***PLOC***
    ***PLOC***A filter can be added by using the where-object command.***PLOC***
    ***PLOC***For more information on filtering see the ***PLOC***[***PLOC***Using the Where-Object***PLOC***](https://technet.microsoft.com/en-us/library/ee177028.aspx)***PLOC*** documentation.***PLOC***
    
    ***PLOC***```powershell
    get-vm | where {$_.State –eq ‘Running’}***PLOC***


 ```
3.  To list all virtual machines in a powered off state, run the following command. This command is a copy of the command from step 2 with the filter changed from ‘Running’ to ‘Off’.

 ```powershell
 get-vm | where {$_.State –eq ‘Off’}

 ```


###***PLOC***Start and shut down virtual machines***PLOC***

1.  ***PLOC***To start a particular virtual machine, run the following command with name of the virtual machine:***PLOC***
    
    ***PLOC***```powershell
    Start-vm –Name <virtual machine name>***PLOC***


 ```

2. To start all currently powered off virtual machines, get a list of those machines and pipe the list to the 'start-vm' command:

  ```powershell
 get-vm | where {$_.State –eq ‘Off’} | start-vm

 ```

1.  ***PLOC***To shut down all running virtual machines, run this:***PLOC***
    
    ***PLOC***```powershell
    get-vm | where {$_.State –eq ‘Running’} | stop-vm***PLOC***


 ```

### Create a VM checkpoint

To create a checkpoint using PowerShell, select the virtual machine using the `get-vm` command and pipe this to the `checkpoint-vm` command. Finally give the checkpoint a name using `-snapshotname`. The complete command will look like the following:

 ```powershell
 get-vm -Name <VM Name> | checkpoint-vm -snapshotname <name for snapshot>

 ```

***PLOC***For example, here is a checkpoint with the name DEMOCP:***PLOC***

!(media\POSH_CP2.png)

###***PLOC***Create a new virtual machine***PLOC***

***PLOC***The following example shows how to create a new virtual machine in the PowerShell Integrated Scripting Environment (ISE).***PLOC***
***PLOC***This is a simple example and could be expanded on to include additional PowerShell features and more advanced VM deployments.***PLOC***

1.  ***PLOC***To open the PowerShell ISE click on start, type ***PLOC********PLOC***PowerShell ISE***PLOC********PLOC***.***PLOC***
2.  ***PLOC***Run the following code to create a virtual machine.***PLOC***
    ***PLOC***See the ***PLOC***[***PLOC***New-VM***PLOC***](https://technet.microsoft.com/en-us/library/hh848537.aspx)***PLOC*** documentation for detailed information on the New-VM command.***PLOC***
    
    ***PLOC***```powershell
    $VMName = "VMNAME"***PLOC***
    
    ***PLOC***$VM = @{
     Name = $VMName 
     MemoryStartupBytes = 2147483648
     Generation = 2
     NewVHDPath = "C:\Virtual Machines\$VMName\$VMName.vhdx"
     NewVHDSizeBytes = 53687091200
     BootDevice = "VHD"
     Path = "C:\Virtual Machines\$VMName "
     SwitchName = (get-vmswitch).Name[0]
    }***PLOC***
    
    ***PLOC***New-VM @VM
    ```***PLOC***

##***PLOC***Wrap up and References***PLOC***

***PLOC***This document has shown some simple steps to explorer the Hyper-V PowerShell module as well as some sample scenarios.***PLOC***
***PLOC***For more information on the Hyper-V PowerShell module, see the ***PLOC***[***PLOC***Hyper-V Cmdlets in Windows PowerShell reference***PLOC***](https://technet.microsoft.com/%5Clibrary/Hh848559.aspx)***PLOC***.***PLOC***


