***PLOC***ms.ContentId: 44b138bb-962f-4474-a0c4-284646a872e2
title: Setup Windows Containers in place***PLOC***

#***PLOC***Preparing a physical machine or an existing virtual machine for Windows Server Containers***PLOC***

***PLOC***In order to create and manage Windows Server Containers, the Windows Server 2016 Technical Preview environment must be prepared.***PLOC***
***PLOC***This guide will walk through configuring Windows Server Containers on bare metal or in an existing virtual machine running Windows Server 2016 Technical Preview.***PLOC***

> ***PLOC***Other getting started guides:***PLOC***
> 

*   ***PLOC***Run Windows Server Containers in ***PLOC***[***PLOC***Azure***PLOC***](./azure_setup.md)***PLOC***.***PLOC***
*   ***PLOC***Run Windows Server Containers in ***PLOC***[***PLOC***a new Hyper-V VM***PLOC***](./container_setup.md)***PLOC***.***PLOC***
    
    *****PLOC***PLEASE READ PRIOR TO INSTALLING THE CONTAINER OS IMAGE:***PLOC********PLOC***  The license terms of the Microsoft Windows Server Pre-Release software (“License Terms”) apply to your use of the Microsoft Windows Container OS Image supplement (the “supplemental software).***PLOC***
    ***PLOC***By downloading and using the supplemental software, you agree to the License Terms, and you may not use it if you have not accepted the License Terms.***PLOC***
    ***PLOC***Both the Windows Server Pre-Release software and the supplemental software are licensed by Microsoft Corporation.***PLOC***

*****PLOC***System (or VM) requirements:***PLOC*****

*   ***PLOC***System running Windows Server Technical Preview 3 Server Core.***PLOC***
*   ***PLOC***10GB available storage for OS Base Image and setup scripts.***PLOC***
*   ***PLOC***Administrator permissions on the machine or VM.***PLOC***

##***PLOC***Setup an existing Virtual Machine or Bare Metal host for Containers***PLOC***

***PLOC***Windows Server Containers require the Container OS Base Image.***PLOC***
***PLOC***We have put together a script that will download and install this for you.***PLOC***
***PLOC***Follow these steps to configure your system as a Windows Server Container Host.***PLOC***

***PLOC***Start a PowerShell session as administrator.***PLOC***
***PLOC***This can be done by running the following command from the command line.***PLOC***

***PLOC***``` powershell
powershell.exe***PLOC***


```

Make sure the title of the windows is "Administrator: Windows PowerShell". If it does not say Administrator, run this command to run with admin priveledges:

``` powershell
start-process powershell -Verb runas

```

***PLOC***Use the following command to download the setup script.***PLOC***
***PLOC***The script can also be manually downloaded from this location - ***PLOC***[***PLOC***Configuration Script***PLOC***](http://aka.ms/setupcontainers)***PLOC***.***PLOC***

***PLOC***``` PowerShell
wget -uri https://aka.ms/setupcontainers -OutFile C:\ContainerSetup.ps1***PLOC***


```

 After the download completes, execute the script.
``` PowerShell
C:\ContainerSetup.ps1

```

***PLOC***The script will then begin to download and configure the Windows Server Container components.***PLOC***
***PLOC***This process may take quite some time due to the large download.***PLOC***
***PLOC***The machine may reboot during the process.***PLOC***
***PLOC***When finished your machine will be configured and ready for you to create and manage Windows Server Containers and Windows Server Container Images with both PowerShell and Docker.***PLOC***

***PLOC***With these items completed your system should be ready for Windows Server Containers.***PLOC***

##***PLOC***Next Steps - Start Using Containers***PLOC***

***PLOC***Now that you are running Windows Server Containers, jump to the following guides to begin working with Windows Server Containers and Windows Server Container images.***PLOC***

[***PLOC***Quick Start: Windows Server Containers and Docker***PLOC***](./manage_docker.md)

[***PLOC***Quick Start: Windows Server Containers and PowerShell***PLOC***](./manage_powershell.md)

-------------------

[***PLOC***Back to Container Home***PLOC***](../containers_welcome.md)[***PLOC***Known Issues for Current Release***PLOC***](../about/work_in_progress.md)


