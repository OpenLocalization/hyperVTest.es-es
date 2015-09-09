***PLOC***ms.ContentId: A6DD6776-614C-4D28-9B83-CB2EDFD263A3
title: Step 2: Install Hyper-V on Windows 10***PLOC***

#***PLOC***Step 2: Install Hyper-V on Windows 10***PLOC***

***PLOC***Hyper-V can be installed using ***PLOC***[***PLOC***Programs and Features***PLOC***](#UsingProgramsandFeatures)***PLOC*** or ***PLOC***[***PLOC***Windows Powershell***PLOC***](#UsingPowerShell)***PLOC***.***PLOC***

##***PLOC***Using Programs and Features***PLOC***

1.  ***PLOC***Right-click the ***PLOC********PLOC***Windows***PLOC********PLOC*** button and then click ***PLOC********PLOC***Programs and Features***PLOC********PLOC***.***PLOC***
    
    !(media\programs_and_features.png)
2.  ***PLOC***Click ***PLOC********PLOC***Turn Windows features on or off***PLOC********PLOC***.***PLOC***
3.  ***PLOC***Select ***PLOC********PLOC***Hyper-V***PLOC********PLOC***, click ***PLOC********PLOC***OK***PLOC*****
    
    !(media\hyper-v_feature_selected.png)
4.  ***PLOC***When the installation is finished, you'll need  to restart the computer.***PLOC***
    
    !(media\restart.png)

##***PLOC***Using PowerShell***PLOC***

***PLOC***For more information, see the PowerShell help for ***PLOC***[***PLOC***Enable-WindowsOptionalFeature***PLOC***](https://technet.microsoft.com/library/hh852172.aspx)***PLOC***.***PLOC***

1.  ***PLOC***Click on the ***PLOC********PLOC***Windows***PLOC********PLOC*** button and search for ***PLOC********PLOC***Windows PowerShell***PLOC********PLOC***.***PLOC***
2.  ***PLOC***Right-click on ***PLOC********PLOC***Windows PowerShell***PLOC********PLOC*** and then click ***PLOC********PLOC***Run as Administrator***PLOC********PLOC***.***PLOC***
3.  ***PLOC***At the Windows Powerhshell prompt, type the following and then press the ***PLOC********PLOC***Enter***PLOC********PLOC*** key:  
    ***PLOC***` PowerShell
    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
    `
4.  ***PLOC***When the installation is finished, restart the computer.***PLOC***

##***PLOC***How do I know Hyper-V installed correctly?***PLOC***

***PLOC***After you restart your computer start the Hyper-V Manager tool.***PLOC***

1.  ***PLOC***Click on the ***PLOC********PLOC***Windows***PLOC********PLOC*** button and type ***PLOC********PLOC***Hyper-V***PLOC********PLOC***.***PLOC***
2.  ***PLOC***Click on ***PLOC********PLOC***Hyper-V Manager***PLOC********PLOC*** in the list.***PLOC***
3.  ***PLOC***The Hyper-V Manager application should start.***PLOC***

##***PLOC***Next Step***PLOC***

[***PLOC***Step 3: Create a virtual switch***PLOC***](walkthrough_virtual_switch.md)


