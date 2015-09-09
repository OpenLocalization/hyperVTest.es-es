***PLOC***ms.ContentId: 71a03c62-50fd-48dc-9296-4d285027a96a
title: Setup Windows Containers in a local VM***PLOC***

#***PLOC***Preparing Windows Server Technical Preview for Windows Server Containers***PLOC***

***PLOC***In order to create and manage Windows Server Containers, the Windows Server 2016 Technical Preview environment must be prepared.***PLOC***
***PLOC***This guide will walk through configuring Windows Server Containers in a Hyper-V Virtual Machine.***PLOC***

> ***PLOC***Other getting started guides:***PLOC***
> 

*   ***PLOC***Run Windows Server Containers in ***PLOC***[***PLOC***Azure***PLOC***](./azure_setup.md)***PLOC***.***PLOC***
*   ***PLOC***Run Windows Server Containers in ***PLOC***[***PLOC***an existing virtual machine***PLOC***](./inplace_setup.md)***PLOC***.***PLOC***
*   ***PLOC***Setup Windows Server Containers ***PLOC***[***PLOC***on a physical Windows Server Core installation***PLOC***](./inplace_setup.md)***PLOC***.***PLOC***
    
    *****PLOC***PLEASE READ PRIOR TO INSTALLING THE CONTAINER OS IMAGE:***PLOC********PLOC***  The license terms of the Microsoft Windows Server Pre-Release software (“License Terms”) apply to your use of the Microsoft Windows Container OS Image supplement (the “supplemental software).***PLOC***
    ***PLOC***By downloading and using the supplemental software, you agree to the License Terms, and you may not use it if you have not accepted the License Terms.***PLOC***
    ***PLOC***Both the Windows Server Pre-Release software and the supplemental software are licensed by Microsoft Corporation.***PLOC***
    
    *   ***PLOC***System running Windows 10 / Windows Server Technical Preview 2 or later.***PLOC***
    *   ***PLOC***Hyper-V role enabled (***PLOC***[***PLOC***see instructions***PLOC***](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install#UsingPowerShell)***PLOC***).***PLOC***
    *   ***PLOC***20GB available storage for container host image, OS Base Image and setup scripts.***PLOC***
    *   ***PLOC***Administrator permissions on the Hyper-V host.***PLOC***

> ***PLOC***Windows Server Containers do not require Hyper-V however to keep things simple this guide assumes that a Hyper-V environment is being used to run the Windows Server Container host.***PLOC***
> 

##***PLOC***Setup a New Container Host on a New Virtual Machine***PLOC***

***PLOC***Windows Server Containers consist of several components such as the Windows Server Container Host and Container OS Base Image.***PLOC***
***PLOC***We have put together a script that will download and configure these items for you.***PLOC***
***PLOC***Follow these steps to deploy a new Hyper-V Virtual Machine and configure this system as a Windows Server Container Host.***PLOC***

***PLOC***Start a PowerShell session as Administrator.***PLOC***
***PLOC***This can be done by right clicking on the PowerShell icon and selecting ‘Run as Administrator’, or by running the following command from any PowerShell session.***PLOC***

***PLOC***``` powershell
start-process powershell -Verb runAs***PLOC***


```

Use the following command to download the configuration script. The script can also be manually downloaded from this location - [Configuration Script](http://aka.ms/newcontainerhost).

``` PowerShell
wget -uri https://aka.ms/newcontainerhost -OutFile New-ContainerHost.ps1

```

***PLOC***Run the following command to create and configure the container host where ***PLOC***`<containerhost>`***PLOC*** will be the virtual machine name and ***PLOC***`<password>`***PLOC*** will be the password assigned to the Administrator account.***PLOC***

***PLOC***``` powershell
.\New-ContainerHost.ps1 –VmName <containerhost> -Password <password>***PLOC***


```

When the script begins you will be asked to read and accept licensing terms.


```

***PLOC***Before installing and using the Windows Server Technical Preview 3 with Containers virtual machine you must:
    1.***PLOC***
***PLOC***Review the license terms by navigating to this link: http://aka.ms/WindowsServerTP3ContainerVHDEula
    2.***PLOC***
***PLOC***Print and retain a copy of the license terms for your records.***PLOC***
***PLOC***By downloading and using the Windows Server Technical Preview 3 with Containers virtual machine you agree to such
license terms.***PLOC***
***PLOC***Please confirm you have accepted and agree to the license terms.***PLOC***
***PLOC***[N] No  [Y] Yes  [?] Help (default is "N"): Y***PLOC***


```

The script will then begin to download and configure the Windows Server Container components. This process may take quite some time due to the large download. When finished your Virtual Machine will be configured and ready for you to create and manage Windows Server Containers and Windows Server Container Images with both PowerShell and Docker.  

You may receive the following message during the Window Server Container host deployment process. 

```

***PLOC***This VM is not connected to the network.***PLOC*** ***PLOC***To connect it, run the following:
Get-VM | Get-VMNetworkAdapter | Connect-VMNetworkAdapter -Switchname <switchname>***PLOC***


```
If you do, check the properties of the virtual machine and connect the virtual machine to a virtual switch. You can also run the following PowerShell command where `<switchname>` is the name of the Hyper-V virtual switch that you would like to connect to the virtual machine.

``` powershell 
Get-VM | Get-VMNetworkAdapter | Connect-VMNetworkAdapter -Switchname <switchname>

```

***PLOC***When the configuration script has completed, start the virtual machine.***PLOC***
***PLOC***The VM is configured with Windows Server 2016 Core and will look like the following.***PLOC***

***PLOC***<center>***PLOC***!(./media/containerhost2.png)***PLOC***</center><br />***PLOC***

***PLOC***Finally log into the virtual machine using the password specified during the configuration process and make sure that the Virtual Machine has a valid IP address.***PLOC***
***PLOC***With these items completed your system should be ready for Windows Server Containers.***PLOC***

##***PLOC***Video Walkthrough***PLOC***

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Configure-Windows-Server-Containers-on-a-Local-System/player" width="800" height="450" allowFullScreen="true" frameBorder="0" scrolling="no" caps_internal_Id="aed8b450-b635-4b70-86c6-cadc39485530" />

##***PLOC***Next Steps - Start Using Containers***PLOC***

***PLOC***Now that you have a Windows Server 2016 system running the Windows Server Container feature jump to the following guides to begin working with Windows Server Containers and Windows Server Container images.***PLOC***

[***PLOC***Quick Start: Windows Server Containers and Docker***PLOC***](./manage_docker.md)

[***PLOC***Quick Start: Windows Server Containers and PowerShell***PLOC***](./manage_powershell.md)

-------------------

[***PLOC***Back to Container Home***PLOC***](../containers_welcome.md)[***PLOC***Known Issues for Current Release***PLOC***](../about/work_in_progress.md)


