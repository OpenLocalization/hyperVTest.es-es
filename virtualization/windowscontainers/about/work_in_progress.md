***PLOC***ms.ContentId: 5bbac9eb-c31e-40db-97b1-f33ea59ac3a3
title: Work in Progress***PLOC***

#***PLOC***Work in Progress***PLOC***

***PLOC***If you don't see your problem addressed here or have questions, post them on the ***PLOC***[***PLOC***forum***PLOC***](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)***PLOC***.***PLOC***

-----------------------

##***PLOC***General functionality***PLOC***

###***PLOC***Windows Container Image must exactly match container host***PLOC***

***PLOC***A Windows Server Container requires an operating system image that matches the container host in respect to build and patch level.***PLOC***
***PLOC***A mismatch will lead to instability and or unpredictable behavior for the container and/or the host.***PLOC***

***PLOC***If you install updates against the Windows container host OS you will need to update the container base OS image to have the matching updates.***PLOC***

*****PLOC***Work Around:***PLOC********PLOC***   
Download and install a container base image matching the OS version and patch level of the container host.***PLOC***

###***PLOC***Commands sporadically fail -- try again***PLOC***

***PLOC***In our testing, commands occasionally need to be run multiple times.***PLOC***
***PLOC***The same principle applies to other actions.***PLOC***
***PLOC***For example, if you create a new file and it doesn't appear, try touching the file.***PLOC***

***PLOC***If you have to do this, let us know via ***PLOC***[***PLOC***the forums***PLOC***](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)***PLOC***.***PLOC***

****PLOC**** Work Around:  ****PLOC*******PLOC***  
Build scripts such that they try commands multiple times.***PLOC***
***PLOC***If a command fails, try again.***PLOC***

###***PLOC***All non-C:/ drives are automatically mapped into new containers***PLOC***

***PLOC***All non-C:/ drives available to the container host are automatically mapped into new running Windows Server Containers.***PLOC***

***PLOC***At this point in time there is no way to selectively map folders into a container, as an interim work around drives are mapped automatically.***PLOC***

****PLOC****Work Around: ****PLOC*******PLOC***  
We're working on it.***PLOC***
***PLOC***In the future there will be folder sharing.***PLOC***

###***PLOC***Windows Server Containers are starting very slowly***PLOC***

***PLOC***If your container is taking more than 30 seconds to start, it may be performing many duplicate virus scans.***PLOC***

***PLOC***Many anti-malware solutions, such as Windows Defender, maybe unnecessarily scanning files with-in container images including all of the OS binaries and files in the container OS image.***PLOC***
***PLOC***This occurs when ever a new container is created and from the anti-malware’s perspective all of the “container’s files” look like new files that have not previously been scanned.***PLOC***
***PLOC***So when processes inside the container attempt to read these files the anti-malware components first scan them before allowing access to the files.***PLOC***
***PLOC***In reality these files were already scanned when the container image was imported or pulled to the server.***PLOC***
***PLOC***In future previews new infrastructure will be in place such that anti-malware solutions, including Windows Defender, will be aware of these situations and can act accordingly to avoid multiple scans.***PLOC***

--------------------------

##***PLOC***Networking***PLOC***

###***PLOC***Number of network compartments per container***PLOC***

***PLOC***In this release we support one network compartment per container.***PLOC***
***PLOC***This means that if you have a container with multiple network adapters, you cannot access the same network port on each adapter (e.g. 192.168.0.1:80 and 192.168.0.2:80 belonging to the same container).***PLOC***

****PLOC****Work Around: ****PLOC*******PLOC***  
If multiple endpoints need to be exposed by a container, use NAT port mapping.***PLOC***

###***PLOC***Windows containers are not getting IPs***PLOC***

***PLOC***If you're connecting to the windows server containers with DHCP VM Switches it's possible for the container host to recieve an IP wwhile the containers do not.***PLOC***

***PLOC***The containers get a 169.254.***PLOC********PLOC****.****PLOC********PLOC*** APIPA IP address.***PLOC***

*****PLOC***Work around:***PLOC********PLOC***
This is a side effect of sharing the kernel.***PLOC***
***PLOC***All containers affectively have the same mac address.***PLOC***

***PLOC***Enable MAC address spoofing on the container host.***PLOC***

***PLOC***This can be achieved using PowerShell***PLOC***


```
Get-VMNetworkAdapter -VMName "[YourVMNameHere]"  | Set-VMNetworkAdapter -MacAddressSpoofing On

```


###***PLOC***Creating file shares does not work in a Container***PLOC***

***PLOC***Currently it is not possible to create a file share within a Container.***PLOC***
***PLOC***If you run ***PLOC***`net share`***PLOC*** you will see an error like this:***PLOC***


```
The Server service is not started.

Is it OK to start it? (Y/N) [Y]: y
The Server service is starting.
The Server service could not be started.

A service specific error occurred: 2182.

More help is available by typing NET HELPMSG 3547.

```

****PLOC****Work Around: ****PLOC*******PLOC***
If you want to copy files into a Container you can use the other way round by running ***PLOC***`net use`***PLOC*** within the Container.***PLOC***
***PLOC***For example:***PLOC***


```
net use S: \\your\sources\here /User:shareuser [yourpassword]

```

--------------------------

##***PLOC***Application compatibility***PLOC***

***PLOC***There are so mnay questions about which applications work and don't work in Windows Server Containers, we decided to break application compatability information into ***PLOC***[***PLOC***its own article***PLOC***](../reference/app_compat.md)***PLOC***.***PLOC***

***PLOC***Some of the most common issues are located here as well.***PLOC***

###***PLOC***WinRM won't start in a Windows Server Container***PLOC***

***PLOC***WinRM starts, throws an error, and stops again.***PLOC***
***PLOC***Errors are not logged in the event log.***PLOC***

*****PLOC***Work Around:***PLOC********PLOC***
Use WMI, ***PLOC***[***PLOC***RDP***PLOC***](#RemoteDesktopAccessOfContainers)***PLOC***, or Enter-PSSession -ContainerID***PLOC***

###***PLOC***Can't install ASP.NET 4.5 or ASP.NET 3.5 with IIS in a container using DISM***PLOC***

***PLOC***Installing IIS-ASPNET45 in a container doesn't work inside a Windows Server container.***PLOC***
***PLOC***The installation progress sticks around 95.5%.***PLOC***

***PLOC***``` PowerShell
Enable-WindowsOptionalFeature -Online -FeatureName IIS-ASPNET45***PLOC***


```

This fails because ASP.NET 4.5 doesn't run in a container.

**Work Around:**  
Instead, install the Web-Server role to use IIS. ASP 5.0 does work. 

``` PowerShell
Enable-WindowsOptionalFeature -Online -FeatureName Web-Server

```

***PLOC***See the ***PLOC***[***PLOC***application compatability article***PLOC***](../reference/app_compat.md)***PLOC*** for more information about what applications can be containerized.***PLOC***

--------------------------

##***PLOC***Docker management***PLOC***

###***PLOC***Docker clients unsecured by default***PLOC***

***PLOC***In this pre-release, docker communication is public if you know where to look.***PLOC***

###***PLOC***Docker commands that don't work with Windows Server Containers***PLOC***

***PLOC***Commands known to fail:***PLOC***

| *****PLOC***Docker command***PLOC*****| *****PLOC***Where it runs***PLOC*****| *****PLOC***Error***PLOC*****| *****PLOC***Notes***PLOC*****|
|:-----|:-----|:-----|:-----|
| *****PLOC***docker commit***PLOC*****| ***PLOC***image***PLOC***| ***PLOC***Docker stops running container and doesn’t show correct error message***PLOC***| ***PLOC***Committing a stopped container works.***PLOC******PLOC***For running containers: We're working on it :)***PLOC***|
| *****PLOC***docker diff***PLOC*****| ***PLOC***daemon***PLOC***| ***PLOC***Error: The windows graphdriver does not support Changes()***PLOC***| |
| *****PLOC***docker kill***PLOC*****| ***PLOC***container***PLOC***| ***PLOC***Error: Invalid signal: KILL  Error: failed to kill containers:[]***PLOC***| |
| *****PLOC***docker load***PLOC*****| ***PLOC***image***PLOC***| ***PLOC***Fails silently***PLOC***| ***PLOC***No error but the image isn't loading either***PLOC***|
| *****PLOC***docker pause***PLOC*****| ***PLOC***container***PLOC***| ***PLOC***Error: Windows container cannot be paused.***PLOC******PLOC***May be not supported***PLOC***| |
| *****PLOC***docker port***PLOC*****| ***PLOC***container***PLOC***| | ***PLOC***No port is getting listed even we are able to RDP.***PLOC***
| *****PLOC***docker pull***PLOC*****| ***PLOC***daemon***PLOC***| ***PLOC***Error: System cannot find the file path.***PLOC******PLOC***We cant run container using this image.***PLOC***| ***PLOC***Image is getting added can't be used.***PLOC******PLOC***We're working on it :)***PLOC***|
| *****PLOC***docker restart***PLOC*****| ***PLOC***container***PLOC***| ***PLOC***Error: A system shutdown is in progress.***PLOC***| |
| *****PLOC***docker unpause***PLOC*****| ***PLOC***container***PLOC***| | ***PLOC***Can't test because pause doesn't work yet.***PLOC***|
***PLOC***If anything that isn't on this list fails (or if a command fails differently than expected), let us know via ***PLOC***[***PLOC***the forums***PLOC***](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)***PLOC***.***PLOC***

###***PLOC***Docker commands that partially work with Windows Server Containers***PLOC***

***PLOC***Commands with partial functionality:***PLOC***

| *****PLOC***Docker command***PLOC*****| *****PLOC***Runs on...***PLOC*****| *****PLOC***Parameter***PLOC*****| *****PLOC***Notes***PLOC*****|
|:-----|:-----|:-----|:-----|
| *****PLOC***docker attach***PLOC*****| ***PLOC***container***PLOC***| ***PLOC***--no-stdin=false***PLOC***| ***PLOC***The command doesn't exit when Ctrl-P and CTRL-Q is pressed***PLOC***|
| | | ***PLOC***--sig-proxy=true***PLOC***| ***PLOC***works***PLOC***|
| *****PLOC***docker build***PLOC*****| ***PLOC***images***PLOC***| ***PLOC***-f, --file***PLOC***| ***PLOC***Error: Unable to prepare context: Unable to get synlinks***PLOC***|
| | | ***PLOC***--force-rm=false***PLOC***| ***PLOC***works***PLOC***|
| | | ***PLOC***--no-cache=false***PLOC***| ***PLOC***works***PLOC***|
| | | ***PLOC***-q, --quiet=false***PLOC***| |
| | | ***PLOC***--rm=true***PLOC***| ***PLOC***works***PLOC***|
| | | ***PLOC***-t, --tag=""***PLOC***| ***PLOC***works***PLOC***|
| *****PLOC***docker login***PLOC*****| ***PLOC***daemon***PLOC***| ***PLOC***-e, -p, -u***PLOC***| ***PLOC***sporratic behavior***PLOC***|
| *****PLOC***docker push***PLOC*****| ***PLOC***daemon***PLOC***| | ***PLOC***Getting occasional "repository does not exit" errors.***PLOC***|
| *****PLOC***docker rm***PLOC*****| ***PLOC***container***PLOC***| ***PLOC***-f***PLOC***| ***PLOC***Error: A system shutdown is in progress.***PLOC***|
***PLOC***If anything that isn't on this list fails, if a command fails differently than expected, or if you find a work around, let us know via ***PLOC***[***PLOC***the forums***PLOC***](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)***PLOC***.***PLOC***

###***PLOC***Pasting commands to interactive Docker session is limited to 50 characters***PLOC***

***PLOC***If you copy a command line into an interactive Docker session, it is currently limited to 50 characters.***PLOC***
***PLOC***The pasted string is simply truncated.***PLOC***

***PLOC***This is not by design, we're working on lifting the restriction.***PLOC***

###***PLOC***net use returns System error 1223 instead of prompting for username or password***PLOC***

***PLOC***Workaround: specify both, the username and password, when running net use.***PLOC***
***PLOC***For example:***PLOC***


```
net use S: \\your\sources\here /User:shareuser [yourpassword]

```


###***PLOC***HCS Shim errors when creating new container images***PLOC***

***PLOC***If you encounter error messages like this:***PLOC***


```
hcsshim::ExportLayer - Win32 API call returned error r1=2147942523 err=The filename, directory name, or volume label syntax is incorrect. layerId=606a2c430fccd1091b9ad2f930bae009956856cf4e6c66062b188aac48aa2e34 flavour=1 folder=C:\ProgramData\docker\windowsfilter\606a2c430fccd1091b9ad2f930bae009956856cf4e6c66062b188aac48aa2e34-1868857733

```

***PLOC***You're hitting an issue addressed by the Zero Day Patch for Windows Server 2016 TP3.***PLOC***
***PLOC***This error can also occur when running the Python-3.4.3.msi installer or node-v0.12.7.msi in a container.***PLOC***

***PLOC***If you hit other hcsshim errors, let us know via ***PLOC***[***PLOC***the forums***PLOC***](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)***PLOC***.***PLOC***

##***PLOC***Accessing windows server container with Remote Desktop***PLOC***

***PLOC***Windows Server Containers can be managed/interacted with through a RDP session.***PLOC***

***PLOC***The following steps are needed to remotely connect to a Windows Server Container using RDP.***PLOC***
***PLOC***It is assumed that the Container is connected to the network via a NAT switch.***PLOC***
***PLOC***This is the default when setting up a Container host through the installation script or creating a new VM in Azure.***PLOC***

****PLOC**** In the Container you want to connect to ****PLOC****

***PLOC***The following steps require either managing the Container using Docker or, when using PowerShell, specifying the ***PLOC***`-RunAsAdministrator`***PLOC*** switch when connecting to the Container.***PLOC***
***PLOC***Please take the following steps in the Container you want to connect to.***PLOC***

1.  ***PLOC***Obtain the Container's IP address***PLOC***


  ```
  ipconfig

  ```

***PLOC***  Returns something similar to this***PLOC***


  ```
  Windows IP Configuration

  Ethernet adapter vEthernet (Virtual Switch-f758a5a9519e1956cc3bef06eb03e5728d3fb61cf6d310246185587be490210a-0):

  Connection-specific DNS Suffix  . :
  Link-local IPv6 Address . . . . . : fe80::91cd:fb4c:4ea5:51df%17
  IPv4 Address. . . . . . . . . . . : 172.16.0.2
  Subnet Mask . . . . . . . . . . . : 255.240.0.0
  Default Gateway . . . . . . . . . : 172.16.0.1

  ```

***PLOC***  Please note the IPv4 Address which is typically in the format 172.16.x.x***PLOC***

1.  ***PLOC***Set the password for the builtin administrator user for the Container***PLOC***


  ```
  net user administrator [yourpassword]

  ```


1.  ***PLOC***Enable the builtin administrator user for the Container***PLOC***


  ```
  net user administrator /active:yes

  ```

****PLOC**** On the Container host ****PLOC****

***PLOC***Since Windows Server has the Windows Firewall with Advanced Security enabled by default we need to open some ports for communication in order for RDP to work.***PLOC***
***PLOC***Additionally a port mapping is created so the Container is reachable through a port on the Container host.***PLOC***

***PLOC***The following steps require a PowerShell launched as Administrator on the Container host.***PLOC***

1.  ***PLOC***Allow the default RDP port through the Windows Advanced Firewall***PLOC***


  ```
  New-NetFirewallRule -Name "RDP" -DisplayName "Remote Desktop Protocol" -Protocol TCP -LocalPort @(3389) -Action Allow

  ```


1.  ***PLOC***Allow an additional port for RDP connection to the Container***PLOC***


  ```
  New-NetFirewallRule -Name "ContainerRDP" -DisplayName "RDP Port for connecting to Container" -Protocol TCP -LocalPort @(3390) -Action Allow

  ```

***PLOC***This step opens up port 3390 on the Container host.***PLOC***
***PLOC***It will be used to open a RDP session to the Container.***PLOC***
***PLOC***If you want to connect to multiple Containers, you can repeat this step while providing additional port numbers.***PLOC***

1.  ***PLOC***Add a port mapping for the existing NAT***PLOC***
    
    ***PLOC***In this step you need the IP address from step 1 within the Container***PLOC***


  ```
  Add-NetNatStaticMapping -NatName ContainerNAT -Protocol TCP -ExternalPort 3390 -ExternalIPAddress 0.0.0.0 -InternalPort 3389 -InternalIPAddress [your container IP]

  ```

***PLOC***  Here you ensure that communication to the Container host which is coming in on port 3390 is redirected to port 3389 on the Container running at the IP address you specify.***PLOC***

****PLOC**** Connect to the container via RDP ****PLOC****

***PLOC***Finally you can connect to the Container using RDP.***PLOC***
***PLOC***In order to do that please run the following command on a system which has the Remote Desktop Client installed (e.g. your system running the Container host VM):***PLOC***


```
mstsc /v:[ContainerHostIP]:3390 /prompt

```

***PLOC***Please specify ***PLOC***`administrator`***PLOC*** as the user name and the password that you chose as the password.***PLOC***

***PLOC***The Remote Desktop Connection will ask you whether you want connect to the system despite certificate errors.***PLOC***
***PLOC***If you select "Yes", the RDP connection will be opened.***PLOC***

*****PLOC***Note:***PLOC********PLOC*** Exiting the container RDP session without logoff may prevent the container from shutting down.***PLOC***
***PLOC***Please make sure to exit the RDP session by typing "logoff" (instead of "exit" or just closing the RDP window) before shutting the container down.***PLOC***

--------------------------

##***PLOC***PowerShell management***PLOC***

###***PLOC***Enter-PSSession has containerid argument, New-PSSession doesn't***PLOC***

***PLOC***This is correct.***PLOC***
***PLOC***We're planning on full cimsession support in the future.***PLOC***

***PLOC***Feel free to voice feature requests in ***PLOC***[***PLOC***the forums***PLOC***](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)***PLOC***.***PLOC***

--------------------------
[Back to Container Home](../containers_welcome.md)


