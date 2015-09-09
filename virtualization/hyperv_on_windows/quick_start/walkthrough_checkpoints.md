***PLOC***ms.ContentId: FBBAADE6-F1A1-4B5C-8FD2-BDCA3FCF81CA
title: Step 6: Experiment with checkpoints***PLOC***

#***PLOC***Step 6: Experiment with checkpoints***PLOC***

***PLOC***Checkpoints are a helpful tool when you want to save the present state of a virtual machine before making a change such as applying an update, installing software, or changing a setting.***PLOC***
***PLOC***If the change causes issues, you can restore the checkpoint and go back.***PLOC***

***PLOC***There are two types of checkpoints:  
***PLOC********PLOC***Production checkpoints***PLOC********PLOC***: Used mainly on servers in production environments.***PLOC***
*****PLOC***Standard checkpoints***PLOC********PLOC***: Used in development or testing environments***PLOC***

***PLOC***Production checkpoints are the default for Hyper-V on Windows 10.***PLOC***

##***PLOC***Change the checkpoint type***PLOC***

***PLOC***We'll start by trying out the older style of checkpoints, ***PLOC********PLOC***standard checkpoints***PLOC********PLOC***.***PLOC***
***PLOC***Since production checkpoints are the default, we need to go into the settings for the VM and change the checkpoint type.***PLOC***

1.  ***PLOC***Right-click on ***PLOC********PLOC***Windows Walkthrough VM***PLOC********PLOC*** and select ***PLOC********PLOC***Settings***PLOC********PLOC***.***PLOC***
2.  ***PLOC***In the ***PLOC********PLOC***Management***PLOC********PLOC*** section, select ***PLOC********PLOC***Checkpoints***PLOC********PLOC***.***PLOC***
3.  ***PLOC***Select ***PLOC********PLOC***Standard checkpoints***PLOC********PLOC***.***PLOC***
    ***PLOC***The dialog should look like this:***PLOC***
    
    !(media/standard1.png)
4.  ***PLOC***Click ***PLOC********PLOC***OK***PLOC********PLOC*** to close the dialog box.***PLOC***

##***PLOC***Open Notepad to test checkpoints***PLOC***

***PLOC***In order to see what happens with each type of checkpoint, we'll run an application in the VM.***PLOC***

1.  ***PLOC***Right-click on ***PLOC********PLOC***Windows Walkthrough VM***PLOC********PLOC*** and select ***PLOC********PLOC***Connect***PLOC********PLOC***.***PLOC***
2.  ***PLOC***In the virtual machine, open ***PLOC********PLOC***Notepad***PLOC********PLOC*** by clicking on the ***PLOC********PLOC***Start***PLOC********PLOC*** menu and typing ***PLOC********PLOC***Notepad***PLOC********PLOC*** and then select it from the results.***PLOC***
3.  ***PLOC***In Notepad, type ***PLOC********PLOC***This is a test of checkpoints.***PLOC********PLOC*** The file should look like this:***PLOC***
    
    !(media/standard_notepad.png)
4.  ***PLOC***Save the file as ***PLOC********PLOC***test.txt***PLOC********PLOC***, but don't close Notepad.***PLOC***
    ***PLOC***Leave it running in the virtual machine.***PLOC***

##***PLOC***Create a standard checkpoint***PLOC***

1.  ***PLOC***To create the checkpoint, click on the ***PLOC***!(media/checkpoint_button.png)*****PLOC***Checkpoint***PLOC********PLOC*** button in the menu bar.***PLOC***
2.  ***PLOC***In the checkpoint name dialog, type ***PLOC********PLOC***Standard***PLOC********PLOC***.***PLOC***
    ***PLOC***The dialog should look like this:***PLOC***
    
    !(media/save_standard.png)
3.  ***PLOC***When the process is complete, the checkpoint will appear under ***PLOC********PLOC***Checkpoints***PLOC********PLOC*** in the ***PLOC********PLOC***Hyper-V Manager***PLOC********PLOC***.***PLOC***
    
    !(media/standard_complete.png)

##***PLOC***Create a production checkpoint***PLOC***

***PLOC***Now, we need to change change the type of checkpoint that we want to take back to ***PLOC********PLOC***Production checkpoints***PLOC********PLOC*** before taking a second checkpoint.***PLOC***

1.  ***PLOC***Right-click the virtual machine, and click ***PLOC********PLOC***Settings***PLOC********PLOC***.***PLOC***
2.  ***PLOC***In the ***PLOC********PLOC***Management***PLOC********PLOC*** section, select ***PLOC********PLOC***Checkpoints***PLOC********PLOC***.***PLOC***
3.  ***PLOC***Select ***PLOC********PLOC***Production checkpoints***PLOC********PLOC***.***PLOC***
4.  ***PLOC***Clear the fall-back option.***PLOC***
    ***PLOC***If the system can't take a production checkpoint, we want it to fail instead of taking a standard checkpoint.***PLOC***
    
    !(media/production.png)
5.  ***PLOC***click ***PLOC********PLOC***OK***PLOC********PLOC*** to close the dialog box.***PLOC***
6.  ***PLOC***Right-click on the VM again and select ***PLOC********PLOC***Connect***PLOC********PLOC***.***PLOC***
7.  ***PLOC***In Notepad in the VM, type another line that reads ***PLOC********PLOC***This is a test of a production checkpoint***PLOC********PLOC*** and save the file again.***PLOC***
8.  ***PLOC***Click on the ***PLOC***!(media/checkpoint_button.png)*****PLOC***Checkpoint***PLOC********PLOC*** button in the menu bar.***PLOC***
9.  ***PLOC***When asked, name it ***PLOC********PLOC***Production***PLOC********PLOC*** and then click ***PLOC********PLOC***Yes***PLOC********PLOC***.***PLOC***
    
    !(media/production_CheckpointName.png)
10.  ***PLOC***Close VMConnect.***PLOC***
    ***PLOC***The VM will continue running, you just won't be connected to it anymore.***PLOC***
11.  ***PLOC***In Hyper-V manager, your list of checkpoints will now look like this:***PLOC***
    
    !(media/production_complete.png)

##***PLOC***Apply the standard checkpoint***PLOC***

1.  ***PLOC***In ***PLOC********PLOC***Hyper-V Manager***PLOC********PLOC***, in the ***PLOC********PLOC***Checkpoints***PLOC********PLOC*** section, right-click the one titled ***PLOC********PLOC***Standard***PLOC********PLOC*** and click ***PLOC********PLOC***Apply***PLOC********PLOC***.***PLOC***
2.  ***PLOC***In the pop-up dialog, click ***PLOC********PLOC***Create Checkpoint and Apply***PLOC********PLOC***.***PLOC***
    
    !(media/apply_standard.png)
3.  ***PLOC***When the finished, your list of checkpoints will now look something like this:***PLOC***
    
    !(media/standard_applied.png)
4.  ***PLOC***When this finishes, right-click the VM and the click ***PLOC********PLOC***Connect***PLOC********PLOC*** to connect to the VM.***PLOC***
5.  ***PLOC***When you connect to the VM, the VM should be running, with Notepad open, but the line about production checkpoints will be missing:***PLOC***
    
    !(media/standard_applied_notepad.png)
6.  ***PLOC***Close VMConnect, but leave the VM running.***PLOC***

##***PLOC***Apply the production checkpoint***PLOC***

***PLOC***Now, let's go back to Hyper-V manager and apply the production checkpoint and see how our VM looks afterwards.***PLOC***

1.  ***PLOC***In the Checkpoints section, right-click the one titled ***PLOC********PLOC***Production Checkpoint***PLOC********PLOC*** and click ***PLOC********PLOC***Apply***PLOC********PLOC***.***PLOC***
2.  ***PLOC***In the pop-up dialog, pick ***PLOC********PLOC***Create Checkpoint and Apply***PLOC********PLOC***.***PLOC***
3.  ***PLOC***When this finishes, right-click the VM and the click ***PLOC********PLOC***Connect***PLOC********PLOC*** to launch the VM.***PLOC***
4.  ***PLOC***You'll notice that the VM is not running.***PLOC***
    ***PLOC***Click on the ***PLOC***!(media/start.png)***PLOC*** Start button in the menu bar to start the VM.***PLOC***
5.  ***PLOC***Open open test.txt in Notepad.***PLOC***
    ***PLOC***You should see the line in the file about testing production checkpoints:***PLOC***
    
    !(media/production_notepad.png)

##***PLOC***Rename a checkpoint***PLOC***

1.  ***PLOC***Right-click the last checkpoint in the tree and click Rename.***PLOC***
2.  ***PLOC***Name the checkpoint ***PLOC********PLOC***Delete me***PLOC********PLOC***.***PLOC***
    
    !(media/delete_me.png)

##***PLOC***Delete a checkpoint***PLOC***

***PLOC***The previous step has probably given you a hint about what we'll do next.***PLOC***
***PLOC***We are going to delete the checkpoint that you just renamed.***PLOC***

1.  ***PLOC***Right-click on the checkpoint named ***PLOC********PLOC***Delete me***PLOC********PLOC*** and click ***PLOC********PLOC***Delete checkpoint***PLOC********PLOC***.***PLOC***
    
    !(media/delete_checkpoint.png)
2.  ***PLOC***In the warning dialog, click ***PLOC********PLOC***Delete***PLOC********PLOC***.***PLOC***
    
    !(media/delete_warn.png)
3.  ***PLOC***After the checkpoint is deleted, your list should look something like this:***PLOC***
    
    !(media/after_delete.png)

##***PLOC***Next Step:***PLOC***

[***PLOC***Step 7: Export and import a virtual machine***PLOC***](walkthrough_export_import.md)


