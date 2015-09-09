***PLOC***ms.ContentId: B971C429-CEF0-4DAB-8456-3B08AEC0C233
title: Step 7: Export and import a virtual machine***PLOC***

#***PLOC***Step 7: Export and import a virtual machine***PLOC***

***PLOC***You can quickly copy a virtual machine or move a virtual machine by using the export and import functionality.***PLOC***

##***PLOC***Export the VM***PLOC***

***PLOC***Exporting a virtual machine exports all of the pieces of the VM, including the checkpoints.***PLOC***

1.  ***PLOC***In Hyper-V Manager, right-click the virtual machine and select ***PLOC********PLOC***Export***PLOC********PLOC***.***PLOC***
    
    !(media/select_export1.png)
2.  ***PLOC***Click ***PLOC********PLOC***Browse***PLOC********PLOC*** in the dialog box and navigate to  C:\Users\Public and then click ***PLOC********PLOC***Select Folder***PLOC********PLOC***.***PLOC***
3.  ***PLOC***In the ***PLOC********PLOC***Export Virtual Machine***PLOC********PLOC*** dialog, make sure the path looks okay and then click ***PLOC********PLOC***Export***PLOC********PLOC***.***PLOC***
    
    !(media/click_export.png)
4.  ***PLOC***While the VM is being exported, you can see the progress in the Status section:***PLOC***
    
    !(media/export_progress.png)

##***PLOC***Did the export work?***PLOC***

***PLOC***To verify that the virtual machine was exported, right-click on your ***PLOC********PLOC***Start***PLOC********PLOC*** menu and select ***PLOC********PLOC***File Explorer***PLOC********PLOC***.***PLOC***

1.  ***PLOC***Navigate to C:\Users\Public\Windows Walkthrough VM.***PLOC***
2.  ***PLOC***You should see another folder called Windows Walkthrough VM and inside that folder should be three folders with the files for your exported virtual machine:***PLOC***
    
    *   ***PLOC***Snapshots***PLOC***
    *   ***PLOC***Virtual Hard Disks***PLOC***
    *   ***PLOC***Virtual Machines ***PLOC***
    
    !(media/export_confirm.png)

##***PLOC***Import the VM***PLOC***

***PLOC***Before we import the VM, we are going to delete the original VM.***PLOC***
***PLOC***Right-click on the VM and select ***PLOC********PLOC***Delete***PLOC********PLOC***.***PLOC***

1.  ***PLOC***In ***PLOC********PLOC***Hyper-V Manager***PLOC********PLOC***, in the ***PLOC********PLOC***Action***PLOC********PLOC*** menu, click ***PLOC********PLOC***Import Virtual Machine***PLOC********PLOC***.***PLOC***
2.  ***PLOC***In the ***PLOC********PLOC***Locate Folder***PLOC********PLOC*** section, click Browse and navigate to C:\Users\Public\Windows Walkthrough VM  and then click ***PLOC********PLOC***Next***PLOC********PLOC***.***PLOC***
3.  ***PLOC***In the ***PLOC********PLOC***Select virtual machine to import***PLOC********PLOC*** screen click ***PLOC********PLOC***Next***PLOC********PLOC***.***PLOC***
4.  ***PLOC***In the ***PLOC********PLOC***Choose Import Type***PLOC********PLOC*** section, select ***PLOC********PLOC***Register the virtual machine in place***PLOC********PLOC*** and then click ***PLOC********PLOC***Next***PLOC********PLOC***.***PLOC***
5.  ***PLOC***In the ***PLOC********PLOC***Choose Destination***PLOC********PLOC*** section, leave the default and click ***PLOC********PLOC***Next***PLOC********PLOC***.***PLOC***
6.  ***PLOC***In Choose Storage folders, leave the default path and click ***PLOC********PLOC***Next***PLOC********PLOC***.***PLOC***
7.  ***PLOC***On the summary page you'll see a list of the paths where the new VM files will be located.***PLOC***
    ***PLOC***Click ***PLOC********PLOC***Finish***PLOC********PLOC*** to start the import.***PLOC***

##***PLOC***Did the import work?***PLOC***

***PLOC***To make sure the import worked, just double-click the VM in ***PLOC********PLOC***Hyper-V Manager***PLOC********PLOC*** and launch VMConnect to check the VM.***PLOC***

##***PLOC***Next Step:***PLOC***

[***PLOC***Step 8: Experiment with Windows Powershell***PLOC***](walkthrough_powershell.md)


