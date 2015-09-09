***PLOC***ms.ContentId: d0a07897-5fd2-41a5-856d-dc8b499c6783
title: Manage Windows Server Containers with PowerShell***PLOC***

#***PLOC***Quick Start: Windows Server Containers and PowerShell***PLOC***

***PLOC***This article will walk through the fundamentals of managing Windows Server Containers with PowerShell.***PLOC***
***PLOC***Items covered will include creating Windows Server Containers and Windows Server Container Images, removing Windows Server Containers and Container Images and finally deploying an application into a Windows Server Container.***PLOC***
***PLOC***The lessons learned in this walkthrough should enable you to begin exploring deployment and management of Windows Server Containers using PowerShell.***PLOC***

***PLOC***Have questions?***PLOC***
***PLOC***Ask them on the ***PLOC***[***PLOC***Windows Containers forum***PLOC***](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)***PLOC***.***PLOC***

> *****PLOC***Note:***PLOC********PLOC*** Windows Server Containers created with PowerShell can not currently be managed with Docker and visa versa.***PLOC***
> ***PLOC***To create containers with Docker instead, see ***PLOC***[***PLOC***Quick Start: Windows Server Containers and Docker***PLOC***](./manage_docker.md)***PLOC***.***PLOC***
> ***PLOC***<br /><br /> If you want to know more, ***PLOC***[***PLOC***read the FAQ***PLOC***](../about/faq.md#WhydoIhavetopickbetweenDockerandPowerShellforWindowsServerContainermanagement)***PLOC***.***PLOC***
> 

##***PLOC***Prerequisites***PLOC***

***PLOC***In order to complete this walkthrough the following items need to be in place.***PLOC***

*   ***PLOC***Windows Server 2016 TP3 or later configured with the Windows Server Containers Feature.***PLOC***
    ***PLOC***If you have completed the setup guide, this is the VM that was created in Azure or Hyper-V.***PLOC***
*   ***PLOC***This system must be connected to a network and able to access the internet.***PLOC***

***PLOC***If you need to configure the container feature, see the following guides: ***PLOC***[***PLOC***Container Setup in Azure***PLOC***](./azure_setup.md)***PLOC*** or ***PLOC***[***PLOC***Container Setup in Hyper-V***PLOC***](./container_setup.md)***PLOC***.***PLOC***

##***PLOC***Basic Container Management with PowerShell***PLOC***

***PLOC***This first example will walk through the basics of creating and removing Windows Server Containers and Windows Server Container Images with PowerShell.***PLOC***

***PLOC***To begin the walk through, log into your Windows Server Container Host System, you will see a Windows command prompt.***PLOC***

!(media/cmd.png)

***PLOC***Start a PowerShell session by typing ***PLOC***`powershell`***PLOC***.***PLOC***
***PLOC***You will know that you are in a PowerShell session when the prompt changes from ***PLOC***`C:\directory>`***PLOC*** to ***PLOC***`PS C:\directory>`***PLOC***.***PLOC***


```
C:\> powershell
Windows PowerShell
Copyright (C) 2015 Microsoft Corporation. All rights reserved.

PS C:\>

```

***PLOC***Use ***PLOC***`Get-Command`***PLOC*** to see the available commands in the containers module***PLOC***


```
PS C:\> Get-Command -Module containers

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Function        Install-ContainerOSImage                           1.0.0.0    Containers
Function        Uninstall-ContainerOSImage                         1.0.0.0    Containers
Cmdlet          Add-ContainerNetworkAdapter                        1.0.0.0    Containers
Cmdlet          Connect-ContainerNetworkAdapter                    1.0.0.0    Containers
Cmdlet          Disconnect-ContainerNetworkAdapter                 1.0.0.0    Containers
Cmdlet          Export-ContainerImage                              1.0.0.0    Containers
Cmdlet          Get-Container                                      1.0.0.0    Containers
Cmdlet          Get-ContainerHost                                  1.0.0.0    Containers
Cmdlet          Get-ContainerImage                                 1.0.0.0    Containers
Cmdlet          Get-ContainerNetworkAdapter                        1.0.0.0    Containers
Cmdlet          Import-ContainerImage                              1.0.0.0    Containers
Cmdlet          Move-ContainerImageRepository                      1.0.0.0    Containers
Cmdlet          New-Container                                      1.0.0.0    Containers
Cmdlet          New-ContainerImage                                 1.0.0.0    Containers
Cmdlet          Remove-Container                                   1.0.0.0    Containers
Cmdlet          Remove-ContainerImage                              1.0.0.0    Containers
Cmdlet          Remove-ContainerNetworkAdapter                     1.0.0.0    Containers
Cmdlet          Set-ContainerNetworkAdapter                        1.0.0.0    Containers
Cmdlet          Start-Container                                    1.0.0.0    Containers
Cmdlet          Stop-Container                                     1.0.0.0    Containers
Cmdlet          Test-ContainerImage                                1.0.0.0    Containers

```

***PLOC***Next make sure that your system has a valid IP Address using ***PLOC***`ipconfig`***PLOC*** and take note of this address for later use.***PLOC***


```
ipconfig

Ethernet adapter Ethernet 3:

   Connection-specific DNS Suffix  . :
   IPv6 Address. . . . . . . . . . . : 2601:600:8f01:84eb::e
   IPv6 Address. . . . . . . . . . . : 2601:600:8f01:84eb:a8c1:a3e:96b7:ffcb
   Link-local IPv6 Address . . . . . : fe80::a8c1:a3e:96b7:ffcb%5
   IPv4 Address. . . . . . . . . . . : 192.168.1.25

```

***PLOC***If you are working from an Azure VM instead of using ***PLOC***`ipconfig`***PLOC*** you will need to get the public IP address of the Azure Virtual Machine.***PLOC***

!(media/newazure9.png)

###***PLOC***Step 1 - Create a New Container***PLOC***

***PLOC***Before creating a Windows Server Container you will need the name of a Container Image and the name of a virtual switch that will be attached to the new container.***PLOC***

***PLOC***Use the ***PLOC***`Get-ContainerImage`***PLOC*** command to return a list of container images loaded on the host.***PLOC***
***PLOC***Take note of the image name that you will use to create the container.***PLOC***
***PLOC***``` PowerShell
Get-ContainerImage***PLOC***

***PLOC***Name              Publisher    Version      IsOSImage
----              ---------    -------      ---------
WindowsServerCore CN=Microsoft 10.0.10514.0 True***PLOC***


```

Use the `Get-VMSwitch` command to return a list of switches available on the host. Take note of the switch name that will be used with the container.

``` PowerShell
Get-VMSwitch

Name           SwitchType NetAdapterInterfaceDescription
----           ---------- ------------------------------
Virtual Switch NAT

```

***PLOC***Run the following command to create a container.***PLOC***
***PLOC***When running ***PLOC***`New-Container`***PLOC*** you will name the container, specify the container image, and select the network switch to use with the container.***PLOC***
***PLOC***Notice in this example that the output is placed in a variable $container.***PLOC***
***PLOC***This will be helpful later in this exercise.***PLOC***

***PLOC***``` PowerShell
$container = New-Container -Name "MyContainer" -ContainerImageName WindowsServerCore -SwitchName "Virtual Switch"***PLOC***


```

To see a list of containers on the host and verify that the container was created, use the `Get-Container` command. Notice that a container has been created with the name of MyContainer, however it has not been started.

``` PowerShell
Get-Container

Name        State Uptime   ParentImageName
----        ----- ------   ---------------
MyContainer Off   00:00:00 WindowsServerCore

```

***PLOC***To start the container, use ***PLOC***`Start-Container`***PLOC*** proivding the name of the container.***PLOC***

***PLOC***``` PowerShell
Start-Container -Name "MyContainer"***PLOC***


```

You can interact with containers using PowerShell remoting commands such as `Invoke-Command`, or `Enter-PSSession`. The example below creates a remote PowerShell session into the container using the `Enter-PSSession` command. This command needs the container id in order to create the remote session. The container id was stored in the `$container` variable when the container was created. 

Notice that once the remote session has been created the command prompt will change to include the first 11 characters of the container id `[2446380e-629]`.

``` PowerShell
Enter-PSSession -ContainerId $container.ContainerId -RunAsAdministrator

[2446380e-629]: PS C:\Windows\system32>

```

***PLOC***A container can be managed very much like a physical or virtual machine.***PLOC***
***PLOC***Command such as ***PLOC***`ipconfig`***PLOC*** to return the IP address of the container, ***PLOC***`mkdir`***PLOC*** to create a directory in the container and PowerShell commands like ***PLOC***`Get-ChildItem`***PLOC*** all work.***PLOC***
***PLOC***Go ahead and make a change to the container such as creating a file or folder.***PLOC***
***PLOC***For example, the following command will create a file which contains network configuration data about the container.***PLOC***

***PLOC***``` PowerShell
ipconfig > c:\ipconfig.txt***PLOC***


```

You can read the contents of the file to ensure the command completed successfully. Notice that the IP address contained in the text file matches that of the container.

``` PowerShell
type c:\ipconfig.txt

Ethernet adapter vEthernet (Virtual Switch-E0D87408-325B-4818-ADB2-2EC7A2005739-0):

   Connection-specific DNS Suffix  . : corp.microsoft.com
   Link-local IPv6 Address . . . . . : fe80::400e:1e0e:591c:beef%18
   IPv4 Address. . . . . . . . . . . : 172.16.0.2
   Subnet Mask . . . . . . . . . . . : 255.240.0.0
   Default Gateway . . . . . . . . . : 172.16.0.1

```

***PLOC***Now that the container has been modified, exit the remote PowerShell session.***PLOC***

***PLOC***``` PowerShell
exit***PLOC***


```

Stop the container by providing the container name to the `Stop-Container` command. When this command has completed, you will be back in control of the container host.

``` PowerShell
Stop-Container -Name "MyContainer"

```


###***PLOC***Step 2 - Create a New Container Image***PLOC***

***PLOC***An image can now be made from this container.***PLOC***
***PLOC***This image will behave like a snapshot of the container and can be re-deployed many times.***PLOC***

***PLOC***To create a new image named 'newimage' use the ***PLOC***`New-ContainerImage`***PLOC*** command.***PLOC***
***PLOC***When using this command you will specify the container to capture, a name for the new image, and additional metadata as seen below.***PLOC***

***PLOC***``` PowerShell
$newimage = New-ContainerImage -ContainerName MyContainer -Publisher Demo -Name newimage -Version 1.0***PLOC***


```

Use `Get-ContainerImage` to return a list of Container Images. Notice that a new image with the name 'newimage' has been created.

``` PowerShell
Get-ContainerImage

Name              Publisher    Version      IsOSImage
----              ---------    -------      ---------
newimage          CN=Demo      1.0.0.0      False
WindowsServerCore CN=Microsoft 10.0.10254.0 True

```


###***PLOC***Step 3 - Create New Container From Image***PLOC***

***PLOC***Now that you have created a customized container image, go ahead and deploy a new container from this image.***PLOC***

***PLOC***Create a container named 'newcontainer' from the container image named 'newimage', output the result to a variable named '$newcontainer'.***PLOC***

***PLOC***``` PowerShell
$newcontainer = New-Container -Name "newcontainer" -ContainerImageName newimage -SwitchName "Virtual Switch"***PLOC***


```

Start the new container.
``` PowerShell
Start-Container $newcontainer

```

***PLOC***Create a remote PowerShell session with the container.***PLOC***
***PLOC***``` PowerShell
Enter-PSSession -ContainerId $newcontainer.ContainerId -RunAsAdministrator***PLOC***


```

Finally notice that this new container contains the ipconfig.txt file created earlier in this exercise.

``` PowerShell
type c:\ipconfig.txt

Ethernet adapter vEthernet (Virtual Switch-E0D87408-325B-4818-ADB2-2EC7A2005739-0):

   Connection-specific DNS Suffix  . : corp.microsoft.com
   Link-local IPv6 Address . . . . . : fe80::400e:1e0e:591c:beef%18
   IPv4 Address. . . . . . . . . . . : 172.16.0.2
   Subnet Mask . . . . . . . . . . . : 255.240.0.0
   Default Gateway . . . . . . . . . : 172.16.0.1

```

***PLOC*** Once you are done working with this container, exit the remote PowerShell session.***PLOC***

***PLOC***``` PowerShell
exit***PLOC***


```

This exercise has shown that an image taken from a modified container will include all modifications. While the example here was a simple file modification, the same would apply if you were to install software into the container such as a web server. Using these methods, custom images can be created that will deploy application ready containers.

### Step 4 - Remove Containers and Container Images

To stop all running containers run the command below. If any containers are in a stopped state when you run this command, you receive a warning, which is ok.

``` PowerShell
Get-Container | Stop-Container

```

***PLOC***Run the following to remove all containers.***PLOC***

***PLOC***``` PowerShell
Get-Container | Remove-Container -Force***PLOC***


```
To remove the container image named 'newimage', run the following.

``` PowerShell
Get-ContainerImage -Name newimage | Remove-ContainerImage -Force

```


##***PLOC***Host a Web Server in a Container***PLOC***

***PLOC***This next example will demonstrate a more practical use case for Windows Server Containers.***PLOC***
***PLOC***The steps included in this exercise will guide you through creating a web server container image that can be used for deploying web applications hosted inside of a Windows Server Container.***PLOC***

###***PLOC***Step 1 – Create Container from the Windows Server Core OS Image***PLOC***

***PLOC***To create a web server container image, you first need to deploy and start a container from the Windows Server Core OS image.***PLOC***
` PowerShell
$container = New-Container -Name webbase -ContainerImageName WindowsServerCore -SwitchName "Virtual Switch"
 `

***PLOC***Start the container.***PLOC***
***PLOC***``` PowerShell
Start-Container $container***PLOC***


```

When the container is up, create a remote PowerShell session with the container.
``` PowerShell
Enter-PSSession -ContainerId $container.ContainerId -RunAsAdministrator

```


###***PLOC***Step 2 - Install Web Server Software***PLOC***

***PLOC***The next step is to install the web server software.***PLOC***
***PLOC***This example will use nginx for Windows.***PLOC***
***PLOC***Use the following commands to automatically download and extract the nginx software to c:\nginx-1.9.3.***PLOC***
*****PLOC***Note***PLOC********PLOC*** that this step will require the container host to be connected to the internet.***PLOC***
***PLOC***If this step produces a connectivity or name resolution error check the network configuration of the container host.***PLOC***

***PLOC***Download the nginx software.***PLOC***
***PLOC***``` PowerShell
wget -uri 'http://nginx.org/download/nginx-1.9.3.zip' -OutFile "c:\nginx-1.9.3.zip"***PLOC***


```

Extract the nginx software.
``` PowerShell
Expand-Archive -Path C:\nginx-1.9.3.zip -DestinationPath c:\ -Force

```

***PLOC***This is all that needs to be completed for the nginx software installation.***PLOC***

***PLOC***Exit the remote PowerShell session.***PLOC***
***PLOC***``` PowerShell
exit***PLOC***


```

Stop the container using the following command. 
``` PowerShell
Stop-Container $container

```


###***PLOC***Step 3 - Create Image from Web Server Container***PLOC***

***PLOC***With the container modified to include the nginx web server software, you can now create an image from this container.***PLOC***
***PLOC***To do so, run the following command:
``` PowerShell
$webserverimage = New-ContainerImage -Container $container -Publisher Demo -Name nginxwindows -Version 1.0***PLOC***


```
When completed, use the `Get-ContainerImage` command to validate that the image has been created.

``` PowerShell
Get-ContainerImage

Name              Publisher    Version      IsOSImage
----              ---------    -------      ---------
nginxwindows      CN=Demo      1.0.0.0      False
WindowsServerCore CN=Microsoft 10.0.10254.0 True

```


###***PLOC***Step 4 - Deploy Web Server Ready Container***PLOC***

***PLOC***To deploy a Windows Server Container based off of the 'nginxwindows' image, use the ***PLOC***`New-Container`***PLOC*** PowerShell command.***PLOC***

***PLOC***``` PowerShell
$webservercontainer = New-Container -Name webserver1 -ContainerImageName nginxwindows -SwitchName "Virtual Switch"***PLOC***


```

Start the container.
``` PowerShell
Start-Container $webservercontainer

```

***PLOC***Create a remote PowerShell session with the new container.***PLOC***
***PLOC***``` PowerShell
Enter-PSSession -ContainerId $webservercontainer.ContainerId -RunAsAdministrator***PLOC***


```

Once working inside the container, the nginx web server can be started and web content staged. To start the nginx web server, change to the nginx installation directory.
``` PowerShell
cd c:\nginx-1.9.3\

```

***PLOC***Start the nginx web server.***PLOC***
***PLOC***``` PowerShell
start nginx***PLOC***


```

And exit this PS-Session.  The web server will keep running.
``` PowerShell
exit

```


###***PLOC***Step 5 - Configure Container Networking***PLOC***

***PLOC***Depending on the configuration of the container host and network, a container will either receive an IP address from a DHCP server or the container host itself using network address translation (NAT).***PLOC***
***PLOC***This guided walk through is configured to use NAT.***PLOC***
***PLOC***In this configuration a port from the container is mapped to a port on the container host.***PLOC***
***PLOC***The application hosted in the container is then accessed through the IP address / name of the container host.***PLOC***
***PLOC***For example if port 80 from the container was mapped to port 55534 on the container host, a typical http request to the application would look like this http://contianerhost:55534.***PLOC***
***PLOC***This allows a container host to run many containers and allow for the applications in these containers to respond to requests using the same port.***PLOC***

***PLOC***For this lab we need to create this port mapping.***PLOC***
***PLOC***In order to do so we will need to know the IP address of the container and the internal (application) and external (container host) ports that will be configured.***PLOC***
***PLOC***For this example let’s keep it simple and map port 80 from the container to port 80 of the host.***PLOC***
***PLOC***Using the ***PLOC***`Add-NetNatStaticMapping`***PLOC*** command, the ***PLOC***`–InternalIPAddress`***PLOC*** will be the IP address of the container which for this walkthrough should be ‘172.16.0.2’.***PLOC***

***PLOC***``` PowerShell
Add-NetNatStaticMapping -NatName "ContainerNat" -Protocol TCP -ExternalIPAddress 0.0.0.0 -InternalIPAddress 172.16.0.2 -InternalPort 80 -ExternalPort 80***PLOC***


```
When the port mapping has been created you will also need to configure an inbound firewall rule for the configured port. To do so for port 80 run the following command. This script can be copied into the VM. 

``` PowerShell
if (!(Get-NetFirewallRule | where {$_.Name -eq "TCP80"})) {
    New-NetFirewallRule -Name "TCP80" -DisplayName "HTTP on TCP/80" -Protocol tcp -LocalPort 80 -Action Allow -Enabled True
}

```

***PLOC***Next if you are working from Azure and have not already created a Virtual Machine endpoint you will need to create one now.***PLOC***
***PLOC***For more information on Azure VM Endpoints see this article: ***PLOC***[***PLOC***Set up Azure VM Endpoints***PLOC***](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-set-up-endpoints/)***PLOC***.***PLOC***

###***PLOC***Step 6 – Access the Container Hosted Website***PLOC***

***PLOC***With the web server container created, you can now checkout the application hosted in the container.***PLOC***
***PLOC***To do so, open up a browser on different machine and enter ***PLOC***`http://containerhost-ipaddress`***PLOC***.***PLOC***
***PLOC***Notice here that you will be browsing to the IP Address of the Container Host and not the container itself.***PLOC***
***PLOC***If you are working from an Azure Virtual Machine this will be the public IP address or Cloud Service name.***PLOC***

***PLOC***If everything has been correctly configured, you will see the nginx welcome page.***PLOC***

!(media/nginx.png)

***PLOC***At this point, feel free to update the website.***PLOC***
***PLOC***Copy in your own sample website, or use a simple ‘Hello World’ sample site that has been created for this demo.***PLOC***
***PLOC***To use the sample you will first need to re-establish a remote PS session with the container.***PLOC***

***PLOC***You will first need to re-create the remote PS session with the container.***PLOC***
***PLOC***``` PowerShell
Enter-PSSession -ContainerId $webservercontainer.ContainerId -RunAsAdministrator***PLOC***


```
Then run the following command to download and replace the index.html file.

``` powershell
wget -uri 'https://raw.githubusercontent.com/Microsoft/Virtualization-Documentation/master/doc-site/virtualization/windowscontainers/quick_start/SampleFiles/index.html' -OutFile "C:\nginx-1.9.3\html\index.html"

```

***PLOC***After the website has been updated, navigate back to ***PLOC***`http://containerhost-ipaddress`***PLOC***.***PLOC***

!(media/hello.png)

##***PLOC***Video Walkthrough***PLOC***

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Deploying-and-Managing-Windows-Server-Containers-with-PowerShell/player" width="800" height="450" allowFullScreen="true" frameBorder="0" scrolling="no" caps_internal_Id="6b3dc51d-8a49-4a88-8478-8cc3f0d17b1e" />

##***PLOC***Next Steps***PLOC***

***PLOC***Now that you have containers set up and an introduction to the tools, go build your own containerized apps.***PLOC***

***PLOC***Here is a more complete ***PLOC***[***PLOC***PowerShell reference***PLOC***](../reference/powershell_overview.md)***PLOC***.***PLOC***

***PLOC***Remember, this is a ***PLOC********PLOC***preview***PLOC********PLOC*** there are bugs and we have a lot of work in progress.***PLOC***
[***PLOC***This page***PLOC***](../about/work_in_progress.md)***PLOC*** contains many of our known issues.***PLOC***

***PLOC***We are also monitoring the ***PLOC***[***PLOC***forums***PLOC***](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)***PLOC*** very closely.***PLOC***

***PLOC***There are also pre-made samples on ***PLOC***[***PLOC***GitHub***PLOC***](https://github.com/Microsoft/Virtualization-Documentation/tree/master/windows-server-container-samples)***PLOC***.***PLOC***

-----------------------------------
[Back to Container Home](../containers_welcome.md)   
[Known Issues for Current Release](../about/work_in_progress.md)


