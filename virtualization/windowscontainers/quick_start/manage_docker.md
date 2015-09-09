***PLOC***ms.ContentId: 347fa279-d588-4094-90ec-8c2fc241f5b6
title: Manage Windows Server Containers with Docker***PLOC***

#***PLOC***Quick Start: Windows Server Containers and Docker***PLOC***

***PLOC***This article will walk through the fundamentals of managing windows Server Containers with Docker.***PLOC***
***PLOC***Items covered will include creating Windows Server Containers and Windows Server Container Images, removing Windows Server Containers and Container Images and finally deploying an application into a Windows Server Container.***PLOC***
***PLOC***The lessons learned in this walkthrough should enable you to begin exploring deployment and management of Windows Server Containers using Docker.***PLOC***

***PLOC***Have questions?***PLOC***
***PLOC***Ask them on the ***PLOC***[***PLOC***Windows Containers forum***PLOC***](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)***PLOC***.***PLOC***

> *****PLOC***Note:***PLOC********PLOC*** Windows Containers created with PowerShell can not currently be managed with Docker and visa versa.***PLOC***
> ***PLOC***To create containers with PowerShell, see  ***PLOC***[***PLOC***Quick Start: Windows Server Containers and PowerShell***PLOC***](./manage_powershell.md)***PLOC***.***PLOC***
> ***PLOC***<br /><br /> If you want to know more, ***PLOC***[***PLOC***read the FAQ***PLOC***](../about/faq.md#WhydoIhavetopickbetweenDockerandPowerShellforWindowsServerContainermanagement)***PLOC***.***PLOC***
> 

##***PLOC***Prerequisites***PLOC***

***PLOC***In order to complete this walkthrough the following items need to be in place.***PLOC***

*   ***PLOC***Windows Server 2016 TP3 or later configured with the Windows Server Container Feature.***PLOC***
    ***PLOC***If you have completed the setup guide, this is the VM that was created in Azure or Hyper-V.***PLOC***
*   ***PLOC***This system must be connected to a network and able to access the internet.***PLOC***

***PLOC***If you need to configure the container feature, see the following guides: ***PLOC***[***PLOC***Container Setup in Azure***PLOC***](./azure_setup.md)***PLOC*** or ***PLOC***[***PLOC***Container Setup in Hyper-V***PLOC***](./container_setup.md)***PLOC***.***PLOC***

##***PLOC***Basic Container Management with Docker***PLOC***

***PLOC***This first example will walk through the basics of creating and removing Windows Server Containers and Windows Server Container Images with Docker.***PLOC***

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


> ***PLOC***This quick start will be focused on Docker commands however some steps such as managing firewall rules and copying files will be run with PowerShell commands.***PLOC***
> ***PLOC***Work through this walkthrough from a PowerShell session.***PLOC***
> 

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

***PLOC***Before creating a Windows Server Container with Docker you will need the name or ID of an exsisitng Windows Server Container image.***PLOC***

***PLOC***To see all images loaded on the container host use the ***PLOC***`docker images`***PLOC*** command.***PLOC***

***PLOC***``` PowerShell
docker images***PLOC***

***PLOC***REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
windowsservercore   latest              9eca9231f4d4        30 hours ago        9.613 GB
windowsservercore   10.0.10254.0        9eca9231f4d4        30 hours ago        9.613 GB***PLOC***


```

Now, use `docker run` To create a new Windows Server Container. This command as seen below will instruct the Docker daemon to create a new container named ‘dockerdemo’ from the image ‘windowsservercore’ and open an interactive (-it) console session (cmd) with the container.

``` PowerShell
docker run -it --name dockerdemo windowsservercore cmd

```

***PLOC***When the command completes you will be working in a console session on the container.***PLOC***

***PLOC***Working in a container is almost identical to working with Windows installed on a virtual or physical machine.***PLOC***
***PLOC***You can run commands such as ***PLOC***`ipconfig`***PLOC*** to return the IP address of the container, ***PLOC***`mkdir`***PLOC*** to create a new directory, or ***PLOC***`powershell`***PLOC*** to start a PowerShell session.***PLOC***
***PLOC***Go ahead and make a change to the container such as creating a file or folder.***PLOC***
***PLOC***For example, the following command will create a file which contains network configuration data about the container.***PLOC***

***PLOC***``` PowerShell
ipconfig > c:\ipconfig.txt***PLOC***


```

You can read the contents of the file to ensure the command completed successfully. Notice that the IP address contained in the text file matches that of the container.

``` PowerShell
type c:\ipconfig.txt

Ethernet adapter vEthernet (Virtual Switch-94a3e12ad262b3059e08edc4d48fca3c8390e38c3b219023d4a0a4951883e658-0):

   Connection-specific DNS Suffix  . : 
   Link-local IPv6 Address . . . . . : fe80::cc1f:742:4126:9530%18
   IPv4 Address. . . . . . . . . . . : 172.16.0.2
   Subnet Mask . . . . . . . . . . . : 255.240.0.0
   Default Gateway . . . . . . . . . : 172.16.0.1

```

***PLOC***Now that the container has been modified, run the following to stop the console session placing you back in the console session of the container host.***PLOC***

***PLOC***``` PowerShell
exit***PLOC***


```

Finally to see a list of containers on the container host use the `docker ps –a` command. Notice from the output that a container named 'dockerdemo' has been created.

``` PowerShell
docker ps -a

CONTAINER ID        IMAGE               COMMAND        CREATED             STATUS                     PORTS     NAMES
4f496dbb8048        windowsservercore   "cmd"          2 minutes ago       Exited (0) 2 minutes ago             dockerdemo

```


###***PLOC***Step 2 - Create a New Container Image***PLOC***

***PLOC***An image can now be made from this container.***PLOC***
***PLOC***This image will behave like a snapshot of the container and can be re-deployed many times.***PLOC***

***PLOC***To create a new image run the following.***PLOC***
***PLOC***This command instructs the Docker engine to create a new image named 'newcontainerimage' that will include all changes made to the 'deckerdemo' container.***PLOC***

***PLOC***``` PowerShell
docker commit dockerdemo newcontainerimage***PLOC***


```

To see all images on the host, run `docker images`. Notice that a new image has been created with the name 'newcontainerimage'.

``` PowerShell
docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
newcontainerimage   latest              4f8ebcf0a334        2 minutes ago       9.613 GB
windowsservercore   latest              9eca9231f4d4        30 hours ago        9.613 GB
windowsservercore   10.0.10254.0        9eca9231f4d4        30 hours ago        9.613 GB

```


###***PLOC***Step 3 - Create New Container From Image***PLOC***

***PLOC***Now that you have a custom container image, deploy a new container named 'newcontainer' from 'newcontainerimage' and open an interactive shell session with the container.***PLOC***

***PLOC***``` PowerShell
docker run –it --name newcontainer newcontainerimage cmd***PLOC***


```

Take a look at the c:\ drive of this new container and notice that the ipconfig.txt file is present.

![](media/docker3.png)

Exit the newly created container to return to the container hosts console session.

``` PowerShell
exit

```

***PLOC***This exercise has shown that an image taken from a modified container will include all modifications.***PLOC***
***PLOC***While the example here was a simple file modification, the same would apply if you were to install software into the container such as a web server.***PLOC***
***PLOC***Using these methods, custom images can be created that will deploy application ready containers.***PLOC***

###***PLOC***Step 4 - Remove Containers and Images***PLOC***

***PLOC***To remove a container after it is no longer needed use the ***PLOC***`docker rm`***PLOC*** command.***PLOC***
***PLOC***The following command will remove the container name 'newcontainer'.***PLOC***

***PLOC***``` PowerShell
docker rm newcontainer***PLOC***


```
To remove container images when they are no longer needed use the `docker rmi` command. You cannot remove an image if it is referenced by an existing container.

The following command removes the container image named 'newcontainerimage'.
``` PowerShell
docker rmi newcontainerimage

Untagged: newcontainerimage:latest
Deleted: 4f8ebcf0a334601e75070a92294d993b0f182abb6f4c88740c75b05093e6acff

```


##***PLOC***Host a Web Server in a Container***PLOC***

***PLOC***This next example will demonstrate a more practical use case for Windows Server Containers.***PLOC***
***PLOC***The steps included in this exercise will guide you through creating a web server container image that can be used for deploying web applications hosted inside of a Windows Server Container.***PLOC***

###***PLOC***Step 1 - Download Web Server Software***PLOC***

***PLOC***Before creating a container image the web server software will need to be downloaded and staged on the container host.***PLOC***
***PLOC***We will be using the nginx for Windows software for this example.***PLOC***
*****PLOC***Note***PLOC********PLOC*** that this step will require the container host to be connected to the internet.***PLOC***
***PLOC***If this step produces a connectivity or name resolution error check the network configuration of the container host.***PLOC***

***PLOC***Run the following command on the container host to create the directory structure that will be used for this example.***PLOC***

***PLOC***``` PowerShell
mkdir c:\build\nginx\source***PLOC***


```

Run this command on the container host to download the nginx software to 'c:\nginx-1.9.3.zip'.

``` PowerShell
wget -uri 'http://nginx.org/download/nginx-1.9.3.zip' -OutFile "c:\nginx-1.9.3.zip"

```

***PLOC***Finally the following command will extract the nginx software to 'C:\build\nginx\source'.***PLOC***

***PLOC***``` PowerShell
Expand-Archive -Path C:\nginx-1.9.3.zip -DestinationPath C:\build\nginx\source -Force***PLOC***


```

### Step 2 - Create Web Server Image
In the previous example, you manually created, updated and captured a container image. This example will demonstrate an automated method for creating container images using a Dockerfile. Dockerfiles contain instructions that the Docker engine uses to build and modify a container, and then commit the container to a container image. 
For more information on dockerfiles, see [Dockerfile reference](https://docs.docker.com/reference/builder/).

Use the following command to create an empty dockerfile.

``` PowerShell
new-item -Type File c:\build\nginx\dockerfile

```

***PLOC***Open the dockerfile with notepad.***PLOC***


```
notepad.exe c:\build\nginx\dockerfile

```

***PLOC***Copy and paste the following text into notepad, save the file and close notepad.***PLOC***

***PLOC***``` PowerShell
FROM windowsservercore
LABEL Description="nginx For Windows" Vendor="nginx" Version="1.9.3"
ADD source /nginx***PLOC***


```

At this point the dockerfile will be in 'c:\build\nginx' and the nginx software extracted to 'c:\build\nginx\source'. 
You are now ready to build the web server container image based on the instructions in the dockerfile. To do this, run the following command on the container host.

``` PowerShell
docker build -t nginx_windows C:\build\nginx

```

***PLOC***This command instructs the docker engine to use the dockerfile located at ***PLOC***`C:\build\nginx`***PLOC*** to create an image named 'nginx_windows'.***PLOC***

***PLOC***The output will look similar to this:***PLOC***

!(media/docker1.png)

***PLOC***When completed, take a look at the images on the host using the ***PLOC***`docker images`***PLOC*** command.***PLOC***
***PLOC***You should see a new image named 'nginx_windows'.***PLOC***
***PLOC***``` PowerShell
docker images***PLOC***

***PLOC***REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE***PLOC***

***PLOC***nginx_windows       latest              d792268338d0        5 seconds ago       9.613 GB
windowsservercore   10.0.10254.0        9eca9231f4d4        35 hours ago        9.613 GB
windowsservercore   latest              9eca9231f4d4        35 hours ago        9.613 GB***PLOC***


```

### Step 3 – Configure Networking for Container Application
Because you will be hosting a website inside of a container a few networking related configurations need to be made. First a firewall rule needs to be created on the container host that will allow access to the website. In this example we will be accessing the site through port 80. Run the following script to create this firewall rule. This script can be copied into the VM. 

``` powershell
if (!(Get-NetFirewallRule | where {$_.Name -eq "TCP80"})) {
    New-NetFirewallRule -Name "TCP80" -DisplayName "HTTP on TCP/80" -Protocol tcp -LocalPort 80 -Action Allow -Enabled True
}

```

***PLOC***Next if you are working from Azure and have not already created a Virtual Machine endpoint you will need to create one now.***PLOC***
***PLOC***For more information on Azure VM Endpoints see this article: ***PLOC***[***PLOC***Set up Azure VM Endpoints***PLOC***](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-set-up-endpoints/)***PLOC***.***PLOC***

###***PLOC***Step 4 - Deploy Web Server Ready Container***PLOC***

***PLOC***To deploy a Windows Server Container based off of the 'nginx_windows' container run the following command.***PLOC***
***PLOC***This will create a new container named 'nginxcontainer' and start an console session on the container.***PLOC***
***PLOC***The –p 80:80 portion of this command creates a port mapping between port 80 on the host to port 80 on the container.***PLOC***

***PLOC***``` powershell
docker run -it --name nginxcontainer -p 80:80 nginx_windows cmd***PLOC***


```
Once working inside the container, the nginx web server can be started and web content staged. To start the nginx web server, change to the nginx installation directory.

``` powershell
cd c:\nginx\nginx-1.9.3

```

***PLOC***Start the nginx web server.***PLOC***
***PLOC***``` powershell
start nginx***PLOC***


```
### Step 5 – Access the Container Hosted Website

With the web server container created, you can now checkout the application hosted in the container. To do so, open up a browser on different machine and enter `http://containerhost-ipaddress`. Notice here that you will be browsing to the IP Address of the Container Host and not the container itself. If you are working from an Azure Virtual Machine this will be the public IP address or Cloud Service name. 

If everything has been correctly configured, you will see the nginx welcome page.

![](media/nginx.png)

At this point, feel free to update the website. Copy in your own sample website, or run the following command in the container to replace the nginx welcome page with a ‘Hello World’ web page.

```powershell
powershell wget -uri 'https://raw.githubusercontent.com/Microsoft/Virtualization-Documentation/master/doc-site/virtualization/windowscontainers/quick_start/SampleFiles/index.html' -OutFile "C:\nginx\nginx-1.9.3\html\index.html"

```

***PLOC***After the website has been updated, navigate back to ***PLOC***`http://containerhost-ipaddress`***PLOC***.***PLOC***

!(media/hello.png)

> *****PLOC***Note:***PLOC********PLOC*** If you would like to change the Docker Daemon settings (such as to change the port it listens to, to connect to a container remotely), you will need to edit the file "C:\ProgramData\docker\runDockerDaemon.cmd" in the container, and then you will need to restart the service with PowerShell, using ***PLOC***`Restart-Service docker`***PLOC***.***PLOC***
> 

##***PLOC***Video Walkthrough***PLOC***

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Deploying-and-Managing-Windows-Server-Containers-with-Docker/player" width="800" height="450" allowFullScreen="true" frameBorder="0" scrolling="no" caps_internal_Id="f7dff546-6452-4527-bcab-6bf7ad5d8479" />

##***PLOC***Next Steps***PLOC***

***PLOC***Now that you have containers set up and an introduction to the tools, go build your own containerized apps.***PLOC***

***PLOC***Remember, this is a ***PLOC********PLOC***preview***PLOC********PLOC*** there are bugs and we have a lot of work in progress.***PLOC***
[***PLOC***This page***PLOC***](../about/work_in_progress.md)***PLOC*** contains many of our known issues.***PLOC***

***PLOC***Be aware that there are some known Docker commands that ***PLOC***[***PLOC***don't work***PLOC***](../about/work_in_progress.md#DockermanagementDockercommandsthatdontworkwithWindowsServerContainers)***PLOC*** and some that only ***PLOC***[***PLOC***partially work***PLOC***](../about/work_in_progress.md#DockermanagementDockercommandsthatpartiallyworkwithWindowsServerContainers)

***PLOC***We are also monitoring the ***PLOC***[***PLOC***forums***PLOC***](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)***PLOC*** very closely.***PLOC***

***PLOC***There are also pre-made samples on ***PLOC***[***PLOC***GitHub***PLOC***](https://github.com/Microsoft/Virtualization-Documentation/tree/master/windows-server-container-samples)***PLOC***.***PLOC***

-----------------------------------
[Back to Container Home](../containers_welcome.md)   
[Known Issues for Current Release](../about/work_in_progress.md)


