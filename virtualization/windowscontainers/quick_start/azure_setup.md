***PLOC***ms.ContentId: 1ab7bfe1-da35-4ff1-916f-936fedf536a0
title: Setup Windows Containers in Azure***PLOC***

#***PLOC***Preparing Microsoft Azure for Windows Server Containers***PLOC***

***PLOC***Before creating and managing Windows Server Containers in Azure you will need to deploy a Windows Server 2016 Technical Preview image which has been pre-configured with the Windows Server Containers feature.***PLOC***
***PLOC***This guide will walk you through this process.***PLOC***

> ***PLOC***Other getting started guides:***PLOC***
> 

*   ***PLOC***Run Windows Server Containers in ***PLOC***[***PLOC***a new Hyper-V virtual machine***PLOC***](./container_setup.md)***PLOC***.***PLOC***
*   ***PLOC***Run Windows Server Containers in ***PLOC***[***PLOC***an existing virtual machine***PLOC***](./inplace_setup.md)
*   ***PLOC***Setup Windows Server Containers ***PLOC***[***PLOC***on a physical Windows Server Core installation***PLOC***](./inplace_setup.md)

##***PLOC***Start Using Azure Portal***PLOC***

***PLOC***If you have an Azure account, skip straight to ***PLOC***[***PLOC***Create a Container Host VM***PLOC***](#CreateacontainerhostVM)***PLOC***.***PLOC***

1.  ***PLOC***Go to ***PLOC***[***PLOC***azure.com***PLOC***](https://azure.com)***PLOC*** and follow the steps for an ***PLOC***[***PLOC***Azure Free Trial***PLOC***](https://azure.microsoft.com/en-us/pricing/free-trial/)***PLOC***.***PLOC***
2.  ***PLOC***Sign in with your Microsoft account.***PLOC***
3.  ***PLOC***When your account is ready to go, sign into the ***PLOC***[***PLOC***Azure Management Portal***PLOC***](https://portal.azure.com)***PLOC***.***PLOC***

##***PLOC***Create a Container Host VM***PLOC***

***PLOC***Click on the following link to start the VM creation process – ***PLOC***[***PLOC***New Windows Server Container Host in Azure***PLOC***](https://portal.azure.com/#gallery/Microsoft.WindowsServer2016TechnicalPreviewwithContainers)***PLOC***.***PLOC***

***PLOC***You can also search for the image in the Azure gallery.***PLOC***

***PLOC***Click on the ***PLOC***`create`***PLOC*** button.***PLOC***

!(./media/newazure1.png)

***PLOC***Give the Virtual Machine a name, select a user name and a password.***PLOC***

!(media/newazure2.png)

***PLOC***Select Optional Configuration > Endpoints > and enter an HTTP endpoint with a private and public port of 80 as seen below.***PLOC***
***PLOC***When completed click ok two times.***PLOC***

!(./media/newazure3.png)

***PLOC***Select the ***PLOC***`create`***PLOC*** button to start the Virtual Machine deployment process.***PLOC***

!(media/newazure2.png)

***PLOC***When the VM deployment is complete, select the connect button to start an RDP session with the Windows Server Container Host.***PLOC***

!(media/newazure6.png)

***PLOC***Log into the VM using the username and password specified during the VM creation wizard.***PLOC***
***PLOC***Once logged in you will be looking at a Windows command prompt.***PLOC***

!(media/newazure7.png)

##***PLOC***Video Walkthrough***PLOC***

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Configure-Windows-Server-Containers-in-Microsoft-Azure/player" width="800" height="450" allowFullScreen="true" frameBorder="0" scrolling="no" caps_internal_Id="5117071f-50b2-4723-9033-79367badc1ad" />

##***PLOC***Next Steps - Start Using Containers***PLOC***

***PLOC***Now that you have a Windows Server 2016 system running the Windows Server Container feature jump to the following guides to begin working with Windows Server Containers and Windows Server Container images.***PLOC***

[***PLOC***Quick Start: Windows Server Containers and Docker***PLOC***](./manage_docker.md)[***PLOC***Quick Start: Windows Server Containers and PowerShell***PLOC***](./manage_powershell.md)

-------------------
[Back to Container Home](../containers_welcome.md)  
[Known Issues for Current Release](../about/work_in_progress.md)


