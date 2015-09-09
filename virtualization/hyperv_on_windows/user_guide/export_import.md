***PLOC***ms.ContentId: 040B1B51-0F25-4295-B317-8CC4DE0A1AFF
title: Export and import virtual machines***PLOC***


#***PLOC***Export and Import virtual machines***PLOC***

***PLOC***You can use the export and import functionality to quickly duplicate virtual machines or to move them from one host to another.***PLOC***
***PLOC***You don't need to export a virtual machine to be able to import it.***PLOC***
***PLOC***You can simply copy a virtual machine and its associated files to the new host, and then use the ***PLOC********PLOC***Import Virtual Machine***PLOC********PLOC*** wizard to specify the location of the files.***PLOC***
***PLOC***This registers the virtual machine with Hyper-V and makes it available to be used.***PLOC***

##***PLOC***Export virtual machines***PLOC***

***PLOC***An easy way to prepare virtual machines to be imported is the ***PLOC********PLOC***Export Virtual Machine***PLOC********PLOC*** wizard.***PLOC***

1.  ***PLOC***In Hyper-V Manager, select one or multiple virtual machines, right-click on your selection and select ***PLOC********PLOC***Export***PLOC********PLOC***.***PLOC***
2.  ***PLOC***Click ***PLOC********PLOC***Browse***PLOC********PLOC*** in the dialog box and choose where you would like to put the exported VM(s) and then click ***PLOC********PLOC***Select Folder***PLOC********PLOC***.***PLOC***
3.  ***PLOC***In the ***PLOC********PLOC***Export Virtual Machine***PLOC********PLOC*** dialog, click ***PLOC********PLOC***Export***PLOC********PLOC***.***PLOC***

***PLOC***For information about using Windows PowerShell to export virtual machines, see ***PLOC***[***PLOC***Export-VM***PLOC***](https://technet.microsoft.com/library/hh848491.aspx)

##***PLOC***Import virtual machines***PLOC***

1.  ***PLOC***In ***PLOC********PLOC***Hyper-V Manager***PLOC********PLOC***, in the ***PLOC********PLOC***Action***PLOC********PLOC*** menu, click ***PLOC********PLOC***Import Virtual Machine***PLOC********PLOC***.***PLOC***
2.  ***PLOC***In the Locate Folder section, click Browse and navigate to where the virtual machine files are located.***PLOC***
    ***PLOC***<!-- to check if this is resolved - this behavior is a bug from my perspective--> Please note that using the wizard you can import one VM at a time and have to select the VM's folder instead of the general export folder.***PLOC***
    ***PLOC***Click ***PLOC********PLOC***Next***PLOC********PLOC*** when finished.***PLOC***
3.  ***PLOC***Select the virtual machine to import and then click ***PLOC********PLOC***Next***PLOC********PLOC***.***PLOC***
4.  ***PLOC***In the Choose Import Type section, you can choose how to import the virtual machine:***PLOC***
    
    *   *****PLOC***Register***PLOC********PLOC*** - Uses the existing unique ID of the virtual machine and registers it in-place.***PLOC***
        ***PLOC***Choose this option if the virtual machines files are already in the correct location.***PLOC***
    *   *****PLOC***Restore***PLOC********PLOC*** - Uses the original virtual machine’s unique ID and also copies the virtual machine files to the default location specified for the host.***PLOC***
    *   *****PLOC***Copy***PLOC********PLOC*** - Creates a new unique ID for the virtual machine and also copies the virtual machine files to the default location specified for the host.***PLOC***
5.  ***PLOC***After selecting how to import the VM, click ***PLOC********PLOC***Next***PLOC********PLOC***.***PLOC***
6.  ***PLOC***In the Choose Destination section, you can choose where to store the files for the virtual machine or leave them in their current location.***PLOC***
    ***PLOC***When you are finished, click ***PLOC********PLOC***Next***PLOC********PLOC***.***PLOC***
7.  ***PLOC***In Choose Storage folders, you can select another place to store the .vhdx file or leave them where they are.***PLOC***
    ***PLOC***When you are finished, click ***PLOC********PLOC***Next***PLOC********PLOC***.***PLOC***
8.  ***PLOC***When you have finished importing the VM, you'll see the summary page describing where the new VM files are located.***PLOC***

***PLOC***The Import Virtual Machine wizard also walks you through the steps of addressing incompatibilities when you import the virtual machine to the new host—so this wizard can help with configuration that is associated with physical hardware, such as memory, virtual switches, and virtual processors.***PLOC***

***PLOC***To import a virtual machine, the wizard does the following:***PLOC***

1.  ***PLOC***Creates a copy of the virtual machine configuration file.***PLOC***
    ***PLOC***This is done as a precaution in case an unexpected restart occurs on the host, such as from a power outage.***PLOC***
2.  ***PLOC***Validates hardware.***PLOC***
    ***PLOC***Information in the virtual machine configuration file is compared to hardware on the new host.***PLOC***
3.  ***PLOC***Compiles a list of errors.***PLOC***
    ***PLOC***This list identifies what needs to be reconfigured and determines which pages appear next in the wizard.***PLOC***
4.  ***PLOC***Displays the relevant pages, one category at a time.***PLOC***
    ***PLOC***The wizard explains each incompatibility to help you reconfigure the virtual machine so it is compatible with the new host.***PLOC***
5.  ***PLOC***Removes the copy of the configuration file.***PLOC***
    ***PLOC***After the wizard does this, the virtual machine is ready to be started.***PLOC***

***PLOC***In addition to the wizard, the Hyper-V module for Windows PowerShell includes cmdlets for importing virtual machines.***PLOC***
***PLOC***For more information, see ***PLOC***[***PLOC***Import-VM***PLOC***](https://technet.microsoft.com/library/hh848495.aspx)***PLOC***.***PLOC***


