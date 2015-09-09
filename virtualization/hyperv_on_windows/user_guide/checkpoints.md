***PLOC***ms.ContentId: 8D89E9D8-2501-46A7-9304-2F19F37AFC85
title: Working with checkpoints***PLOC***

#***PLOC***Using checkpoints to revert virtual machines to a previous state***PLOC***

***PLOC***Checkpoints provide a fast and easy way to revert the virtual machine to a previous state.***PLOC***
***PLOC***This is especially helpful when you are about to make a change to a virtual machine and you want to be able to roll-back to the present state if that change cause issues.***PLOC***

##***PLOC***Enable or disable checkpoints***PLOC***

1.  ***PLOC***In ***PLOC********PLOC***Hyper-V Manager***PLOC********PLOC***, right-click the name of the virtual machine, and click ***PLOC********PLOC***Settings***PLOC********PLOC***.***PLOC***
2.  ***PLOC***In the ***PLOC********PLOC***Management***PLOC********PLOC*** section, select ***PLOC********PLOC***Checkpoints***PLOC********PLOC***.***PLOC***
3.  ***PLOC***To allow checkpoints to be taken off this virtual machine, make sure Enable Checkpoints is selected -- this is the default behavior.***PLOC***
    ***PLOC***To disable checkpoints, deselect the ***PLOC********PLOC***Enable Checkpoints***PLOC********PLOC*** check box.***PLOC***
4.  ***PLOC***Click ***PLOC********PLOC***Apply***PLOC********PLOC*** to apply your changes.***PLOC***
    ***PLOC***If you are done, click ***PLOC********PLOC***OK***PLOC********PLOC*** to close the dialog box.***PLOC***

##***PLOC***Choose standard or production checkpoints***PLOC***

***PLOC***There are two types of checkpoints:***PLOC***

*   *****PLOC***Production checkpoints***PLOC********PLOC*** -- Used mainly on servers in production environments as a form of backup.***PLOC***
*   *****PLOC***Standard checkpoints***PLOC********PLOC*** -- Used in development or testing environments to allow rollback if a change fails.***PLOC***

***PLOC***Both types of checkpoints restore a virtual machine to a previous state.***PLOC***

***PLOC***Production checkpoints create an application-consistent checkpoint of a virtual machine.***PLOC***
***PLOC***That means the saved virtual machine will resume with no application state.***PLOC***

***PLOC***Standard checkpoints (formerly known as snapshots) capture the exact memory state of your virtual machine.***PLOC***
***PLOC***That means the virtual machine will restore with ***PLOC********PLOC***exactly***PLOC********PLOC*** the same state in which the checkpoint was taken down to the exact application state.***PLOC***
***PLOC***Standard checkpoints may contain information about client connections, transactions, and the external network state.***PLOC***
***PLOC***This information may not be valid when the checkpoint is applied.***PLOC***
***PLOC***Additionally, if a checkpoint is taken during an application crash, restoring that checkpoint will be in the middle of that crash.***PLOC***

***PLOC***The presence of a standard checkpoint for a virtual machine may impact the disk performance of the virtual machine.***PLOC***
***PLOC***We do not recommend using standard checkpoints on virtual machines when performance or the availability of storage space is critical.***PLOC***

***PLOC***Applying a production checkpoint involves booting the guest operating system from an offline state.***PLOC***
***PLOC***This means that no application state or security information is captured as part of the checkpoint process.***PLOC***

***PLOC***The following table shows when to use production checkpoints or standard checkpoints, depending on the state of the virtual machine.***PLOC***

| *****PLOC***Virtual Machine State***PLOC*****| *****PLOC***Production Checkpoint***PLOC*****| *****PLOC***Standard Checkpoint***PLOC*****|
|:-----|:-----|:-----|
| *****PLOC***Running with Integration Services***PLOC*****| ***PLOC***Yes***PLOC***| ***PLOC***Yes***PLOC***|
| *****PLOC***Running without Integration Services***PLOC*****| ***PLOC***No***PLOC***| ***PLOC***Yes***PLOC***|
| *****PLOC***Offline - no saved state***PLOC*****| ***PLOC***Yes***PLOC***| ***PLOC***Yes***PLOC***|
| *****PLOC***Offline - with saved state***PLOC*****| ***PLOC***No***PLOC***| ***PLOC***Yes***PLOC***|
| *****PLOC***Paused***PLOC*****| ***PLOC***No***PLOC***| ***PLOC***Yes***PLOC***|
***PLOC***To see the difference between Standard and Production checkpoints, look at the ***PLOC***[***PLOC***checkpoints walkthrough***PLOC***](../quick_start/walkthrough_checkpoints.md)***PLOC***.***PLOC***

##***PLOC***Set a default checkpoint type***PLOC***

1.  ***PLOC***In ***PLOC********PLOC***Hyper-V Manager***PLOC********PLOC***, right-click the name of the virtual machine, and click ***PLOC********PLOC***Settings***PLOC********PLOC***.***PLOC***
2.  ***PLOC***In the ***PLOC********PLOC***Management***PLOC********PLOC*** section, select ***PLOC********PLOC***Checkpoints***PLOC********PLOC***.***PLOC***
3.  ***PLOC***Select either production checkpoints or standard checkpoints.***PLOC***
    ***PLOC***If you choose production checkpoints, you can also specify whether the host should take a standard checkpoint if a production checkpoint cannot be taken.***PLOC***
    ***PLOC***If you clear this check box and a production checkpoint cannot be taken, no checkpoint will be selected.***PLOC***
4.  ***PLOC***If you want to change the location where the configuration files for the checkpoint are stored, change the path in the ***PLOC********PLOC***Checkpoint File Location***PLOC********PLOC*** section.***PLOC***
5.  ***PLOC***Click ***PLOC********PLOC***Apply***PLOC********PLOC*** to apply your changes.***PLOC***
    ***PLOC***If you are done, click ***PLOC********PLOC***OK***PLOC********PLOC*** to close the dialog box.***PLOC***

***PLOC***The default behavior in Windows 10 for new virtual machines is to create production checkpoints with fallback to standard checkpoints***PLOC***

##***PLOC***Create a checkpoint***PLOC***

***PLOC***To create a checkpoint***PLOC***

1.  ***PLOC***In ***PLOC********PLOC***Hyper-V Manager***PLOC********PLOC***, under ***PLOC********PLOC***Virtual Machines***PLOC********PLOC***, select the virtual machine.***PLOC***
2.  ***PLOC***Right-click the name of the virtual machine, and then click ***PLOC********PLOC***Checkpoint***PLOC********PLOC***.***PLOC***
3.  ***PLOC***When the process is complete, the checkpoint will appear under ***PLOC********PLOC***Checkpoints***PLOC********PLOC*** in the ***PLOC********PLOC***Hyper-V Manager***PLOC********PLOC***.***PLOC***

##***PLOC***Apply a checkpoint***PLOC***

***PLOC***If you want to revert your virtual machine to a previous point-in-time, you can apply an existing checkpoint.***PLOC***

1.  ***PLOC***In ***PLOC********PLOC***Hyper-V Manager***PLOC********PLOC***, under ***PLOC********PLOC***Virtual Machines***PLOC********PLOC***, select the virtual machine.***PLOC***
2.  ***PLOC***In the Checkpoints section, right-click the checkpoint that you want to use and click ***PLOC********PLOC***Apply***PLOC********PLOC***.***PLOC***
3.  ***PLOC***A dialog box appears with the following options: ***PLOC***


```
**Create Checkpoint and Apply**: Creates a new checkpoint of the virtual machine before it applies the earlier checkpoint. 

**Apply**: Applies only the checkpoint that you have chosen. You cannot undo this action.

**Cancel**: Closes the dialog box without doing anything.

```


##***PLOC***Delete a checkpoint***PLOC***

***PLOC***To cleanly delete a checkpoint: ***PLOC***

1.  ***PLOC***In ***PLOC********PLOC***Hyper-V Manager***PLOC********PLOC***, select the virtual machine.***PLOC***
2.  ***PLOC***In the ***PLOC********PLOC***Checkpoints***PLOC********PLOC*** section, right-click the checkpoint that you want to delete, and click Delete.***PLOC***
    ***PLOC***You can also delete a checkpoint and all subsequent checkpoints.***PLOC***
    ***PLOC***To do so, right-click the earliest checkpoint that you want to delete, and then click ***PLOC********PLOC*****Delete Checkpoint***PLOC********PLOC*** Subtree**.***PLOC***
3.  ***PLOC***You might be asked to verify that you want to delete the checkpoint.***PLOC***
    ***PLOC***Confirm that it is the correct checkpoint, and then click ***PLOC********PLOC***Delete***PLOC********PLOC***.***PLOC***
4.  ***PLOC***The .avhdx and .vhdx files will merge, and when complete, the .avhdx file will be deleted from the file system.***PLOC***

> *****PLOC***Tip:***PLOC********PLOC*** You can use Windows Powershell to delete a checkpoint by using the ***PLOC********PLOC***Remove-VMSnapshot***PLOC********PLOC*** cmdlet.***PLOC***
> 

***PLOC***Checkpoints are stored as .avhdx files in the same location as the .vhdx files for the virtual machine.***PLOC***
***PLOC***You should not delete the .avhdx files directly.***PLOC***

##***PLOC***Change where checkpoint settings and save state files are stored***PLOC***

***PLOC***If the virtual machine has no checkpoints, you can change where the checkpoint configuration and saved state files are stored.***PLOC***

1.  ***PLOC***In ***PLOC********PLOC***Hyper-V Manager***PLOC********PLOC***, right-click the name of the virtual machine, and click ***PLOC********PLOC***Settings***PLOC********PLOC***.***PLOC***
2.  ***PLOC***In the ***PLOC********PLOC***Management***PLOC********PLOC*** section, select ***PLOC********PLOC***Checkpoints***PLOC********PLOC*** or ***PLOC********PLOC***Checkpoint File Location***PLOC********PLOC***.***PLOC***
3.  ***PLOC***In ***PLOC********PLOC***Checkpoint File Location***PLOC********PLOC***, enter the path to the folder where you would like to store the files.***PLOC***
4.  ***PLOC***Click ***PLOC********PLOC***Apply***PLOC********PLOC*** to apply your changes.***PLOC***
    ***PLOC***If you are done, click ***PLOC********PLOC***OK***PLOC********PLOC*** to close the dialog box.***PLOC***

***PLOC***The default location for storing checkpoint configuration files is: %systemroot%\ProgramData\Microsoft\Windows\Hyper-V\Snapshots.***PLOC***


##***PLOC***Rename a checkpoint***PLOC***

1.  ***PLOC***In ***PLOC********PLOC***Hyper-V Manager***PLOC********PLOC***, select the virtual machine.***PLOC***
2.  ***PLOC***Right-click the checkpoint, and then select ***PLOC********PLOC***Rename***PLOC********PLOC***.***PLOC***
3.  ***PLOC***Enter in the new name for the checkpoint.***PLOC***
    ***PLOC***It must be less than 100 characters, and the field cannot be empty.***PLOC***
4.  ***PLOC***Click ***PLOC********PLOC***ENTER***PLOC********PLOC*** when you are done.***PLOC***

***PLOC***By default, the name of a checkpoint is the name of the virtual machine combined with the date and time the checkpoint was taken.***PLOC***
***PLOC***This is the standard format:***PLOC***


```
virtual_machine_name (MM/DD/YYY –hh:mm:ss AM\PM)

```

***PLOC***Names are limited to 100 characters or less, and the name cannot be blank.***PLOC***


