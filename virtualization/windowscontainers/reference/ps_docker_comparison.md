***PLOC***ms.ContentId: 4981828d-1a08-4d8c-a99d-874a926a153f
title: PowerShell to Docker Comparison***PLOC***

#***PLOC***PowerShell to Docker comparison for managing Windows Server Containers***PLOC***

***PLOC***There are many ways to manage Windows Server Containers using both in-box Windows tools (PowerShell, in this preview) and Open Source management tools such as Docker.***PLOC***
***PLOC***Guides outlining both individually available here:***PLOC***

*   [***PLOC***Manage Windows Server Containers with Docker***PLOC***](../quick_start/manage_docker.md)
*   [***PLOC***Manage Windows Server Containers with PowerShell***PLOC***](../quick_start/manage_powershell.md)

***PLOC***This page is a more in depth reference comparing the Docker tools and PowerShell management tools.***PLOC***

##***PLOC***PowerShell for containers versus Hyper-V VMs***PLOC***

***PLOC***You can create, run, and interact with Windows Server Containers using PowerShell cmdlets.***PLOC***
***PLOC***Everything you need to get going is available in-box.***PLOC***

***PLOC***If you’ve used Hyper-V PowerShell, the design of the cmdlets should be pretty familiar to you.***PLOC***
***PLOC***A lot of the workflow is similar to how you’d manage a virtual machine using the Hyper-V module.***PLOC***
***PLOC***Instead of ***PLOC***`New-VM`***PLOC***, ***PLOC***`Get-VM`***PLOC***, ***PLOC***`Start-VM`***PLOC***, ***PLOC***`Stop-VM`***PLOC***, you have ***PLOC***`New-Container`***PLOC***, ***PLOC***`Get-Container`***PLOC***, ***PLOC***`Start-Container`***PLOC***, ***PLOC***`Stop-Container`***PLOC***.***PLOC***
***PLOC***There are quite a few container-specific cmdlets and parameters, but the general lifecycle and management of a Windows container looks roughly like that of a Hyper-V VM.***PLOC***

##***PLOC***How does PowerShell management compare to Docker?***PLOC***

***PLOC***The Containers PowerShell cmdlets expose an API that isn’t quite the same as Docker's; as a general rule, the cmdlets are more granular in operation.***PLOC***
***PLOC***Some Docker commands have pretty straightforward parallels in PowerShell:***PLOC***

| ***PLOC***Docker command***PLOC***| ***PLOC***PowerShell Cmdlet***PLOC***|
|----|----|
| `docker ps -a`| `Get-Container`|
| `docker images`| `Get-ContainerImage`|
| `docker rm`| `Remove-Container`|
| `docker rmi`| `Remove-ContainerImage`|
| `docker create`| `New-Container`|
| `docker commit <container ID>`| `New-ContainerImage -Container <container>`|
| `docker load <tarball>`| `Import-ContainerImage <AppX package>`|
| `docker save`| `Export-ContainerImage`|
| `docker start`| `Start-Container`|
| `docker stop`| `Stop-Container`|
***PLOC***The PowerShell cmdlets are not an exact perfect parity, and there are a fair number of commands that we’re not providing PowerShell replacements for* (notably ***PLOC***`docker build`***PLOC*** and ***PLOC***`docker cp`***PLOC***).***PLOC***
***PLOC***But what might leap out at you is that there’s no single one-line replacement for ***PLOC***`docker run`***PLOC***.***PLOC***

***PLOC***\* Subject to change.***PLOC***

###***PLOC***But I need docker run!***PLOC*** ***PLOC***What’s going on?***PLOC***

***PLOC***We’re doing a couple things here to provide a slightly more familiar interaction model for users who know their way around PowerShell already.***PLOC***
***PLOC***Of course, if you’re used to the way docker operates, this will be a bit of a mental shift.***PLOC***

1.  ***PLOC***The lifecycle of a container in the PowerShell model is slightly different.***PLOC***
    ***PLOC***In the Containers PowerShell module, we expose the more granular operations of ***PLOC***`New-Container`***PLOC*** (which creates a new container that’s stopped) and ***PLOC***`Start-Container`***PLOC***.***PLOC***
    
    ***PLOC***In between creating and starting the container, you can also configure the container’s settings; for TP3, the only other configuration we’re planning to expose is the ability to set the network connection for the container.***PLOC***
    ***PLOC***using the (Add/Remove/Connect/Disconnect/Get/Set)-ContainerNetworkAdapter cmdlets.***PLOC***
2.  ***PLOC***You can’t currently pass a command to be run inside the container on start.***PLOC*** ***PLOC***However, you can still get an interactive PowerShell session to a running container using***PLOC*** `Enter-PSSession -ContainerId <ID of a running container>`***PLOC***, and you can execute a command inside a running container using ***PLOC***`Invoke-Command -ContainerId <container id> -ScriptBlock { code to run inside the container }`***PLOC*** or ***PLOC***`Invoke-Command -ContainerId <container id> -FilePath <path to script>`***PLOC***.***PLOC***  
    ***PLOC***Both of these commands allow the optional***PLOC*** `-RunAsAdministrator` ***PLOC***flag for high privilige actions.***PLOC***  

##***PLOC***Caveats and known issues***PLOC***

1.  ***PLOC***Right now, the Containers cmdlets have no knowledge about any containers or images created through Docker, and Docker does not know anything about containers and images created through the PowerShell.***PLOC***
    ***PLOC***If you created it in Docker, manage it with Docker; if you created it through PowerShell, manage it through PowerShell.***PLOC***
2.  ***PLOC***We have quite a bit of work we'd like to do to improve the end user experience -- better error messages, better progress reporting, invalid event strings, and so forth.***PLOC***
    ***PLOC***If you happen to run into a situation where you wish you were getting more or better info, please feel free to send suggestions to the forums.***PLOC***

##***PLOC***A quick runthrough***PLOC***

***PLOC***Here is a walk through of some common workflows.***PLOC***

***PLOC***This assumes you've installed an OS container image named "ServerDatacenterCore" and created a virtual switch named "Virtual Switch" (using New-VMSwitch).***PLOC***

***PLOC***``` PowerShell***PLOC***

###***PLOC***1. Enumerating images***PLOC***

#***PLOC***At this point, you can enumerate the images on the system:***PLOC***

***PLOC***Get-ContainerImage***PLOC***

#***PLOC***Get-ContainerImage also accepts filters.***PLOC***

#***PLOC***For example, this will return all container images whose Name starts with S (case-insensitive):***PLOC***

***PLOC***Get-ContainerImage -Name S****PLOC***

#***PLOC***You can save the results of this to a variable.***PLOC***

#***PLOC***(If you're not familiar with PowerShell, the "$" denotes a variable.)***PLOC***

***PLOC***$baseImage = Get-ContainerImage -Name ServerDatacenterCore
$baseImage***PLOC***

###***PLOC***2. Creating and enumerating containers***PLOC***

#***PLOC***Now, we can create a new container using this image:***PLOC***

***PLOC***New-Container -Name "MyContainer" -ContainerImage $baseImage -SwitchName "Virtual Switch"***PLOC***

#***PLOC***Now we can enumerate all containers.***PLOC***

***PLOC***Get-Container***PLOC***

#***PLOC***Similarly, we can save this container to a variable:***PLOC***

***PLOC***$container1 = Get-Container -Name "MyContainer"***PLOC***

###***PLOC***3. Starting containers, interacting with running containers, and stopping containers***PLOC***

#***PLOC***Now let's go ahead and start the container.***PLOC***

***PLOC***Start-Container -Name "MyContainer"***PLOC***

#***PLOC***(We could've also started this container using "Start-Container -Container $container1".)***PLOC***

#***PLOC***With the container now running, let's go ahead and enter an interactive PowerShell session:***PLOC***

***PLOC***Enter-PSSession -ContainerId $container1.Id***PLOC***

#***PLOC***This should eventually bring up a PowerShell prompt from inside the container.***PLOC***

#***PLOC***You can try all the things that you did in the interactive cmd prompt given by "docker run -it".***PLOC***

#***PLOC***For now, just to prove we've been here, we can create a new file:***PLOC***

***PLOC***cd \
mkdir Test
cd Test
echo "hello world" > hello.txt
exit***PLOC***

#***PLOC***Now we should be back in the outside world.***PLOC*** ***PLOC***Even though we've exited the PowerShell session,***PLOC***

#***PLOC***the container itself is still running, as you can see by printing out the container again:***PLOC***

***PLOC***$container1***PLOC***

#***PLOC***Before we can commit this container to a new image, we need to stop the container.***PLOC***

#***PLOC***Let's do that now.***PLOC***

***PLOC***Stop-Container -Container $container1***PLOC***

###***PLOC***4. Creating a new container image***PLOC***

#***PLOC***And now let's commit it to a new image.***PLOC***

***PLOC***$image1 = New-ContainerImage -Container $container1 -Publisher Test -Name Image1 -Version 1.0***PLOC***

#***PLOC***Enumerate all the images again, for sanity's sake:***PLOC***

***PLOC***Get-ContainerImage***PLOC***

#***PLOC***Rinse and repeat!***PLOC*** ***PLOC***Make another container based on the new image.***PLOC***

***PLOC***$container2 = New-Container -Name "MySecondContainer" -ContainerImage $image1 -SwitchName "Virtual Switch"***PLOC***

#***PLOC***(If you like, you can start the second container and verify that the new file***PLOC***

#***PLOC***"\Test\hello.txt" is there as expected.)***PLOC***

###***PLOC***5. Removing a container***PLOC***

#***PLOC***The first container we created is now stopped.***PLOC*** ***PLOC***Let's get rid of it:***PLOC***

***PLOC***Remove-Container -Container $container1***PLOC***

#***PLOC***And confirm that it's gone:***PLOC***

***PLOC***Get-Container***PLOC***

###***PLOC***6. Exporting, removing, and importing images***PLOC***

#***PLOC***For images that aren't the base OS image, we can export them into an .appx package file.***PLOC***

***PLOC***Export-ContainerImage -Image $image1 -Path "C:\exports"***PLOC***

#***PLOC***This should create a .appx file in the C:\exports folder.***PLOC***

#***PLOC***If you've given your image the same publisher, name, and version we used earlier,***PLOC***

#***PLOC***you'd expect the resulting .appx to be named "CN=Test_Image1_1.0.0.0.appx".***PLOC***

#***PLOC***Before we can try importing the image again, we need to remove the image.***PLOC***

#***PLOC***(If you have any running containers that depend on this image, you'll want to stop them first.)***PLOC***

***PLOC***Remove-ContainerImage -Image $image1***PLOC***

#***PLOC***Now let's import the image again:***PLOC***

***PLOC***Import-ContainerImage -Path C:\exports\CN=Test***PLOC***_***PLOC***Image1***PLOC***_***PLOC***1.0.0.0.appx***PLOC***

#***PLOC***We'd previously created a container dependent on this image.***PLOC*** ***PLOC***You should be able to start it:***PLOC***

***PLOC***Start-Container -Container $container2 ***PLOC***


```

### Build your own sample
You can see all the Containers cmdlets using `Get-Command -Module Containers`.  There are several other cmdlets that are not described here, which we'll leave to you to learn about on your own.    
**Note** This won't return the `Enter-PSSession` and `Invoke-Command` cmdlets, which are part of core PowerShell.

You can also get help about any cmdlet using `Get-Help [cmdlet name]`, or equivalently `[cmdlet name] -?`.  Today, the help output is auto-generated and just tells you the syntax for commands; we will be adding further documentation as we get closer to finalizing the cmdlet design.

A nicer way to discover the syntax is the PowerShell ISE, which you may not have looked at before if you haven't used PowerShell very much. If you're running on a SKU that permits it, try starting the ISE, opening the Commands pane, and choosing the "Containers" module, which will show you a graphical representation of the cmdlets and their parameter sets.

PS: Just to prove it can be done, here's a PowerShell function that composes some of the cmdlets we've seen already into an ersatz `docker run`. (To be clear, this is a proof of concept, not under active development.)

``` PowerShell
function Run-Container ([string]$ContainerImageName, [string]$Name="fancy_name", [switch]$Remove, [switch]$Interactive, [scriptblock]$Command) {
    $image = Get-ContainerImage -Name $ContainerImageName
    $container = New-Container -Name $Name -ContainerImage $image
    Start-Container $container

    if ($Interactive) {
         Start-Process powershell ("-NoExit", "-c", "Enter-PSSession -ContainerId $($container.Id)") -Wait
    } else {
        Invoke-Command -ContainerId $container.Id -ScriptBlock $Command
    }

    Stop-Container $container

    if ($Remove) {
        Remove-Container $container -Force
    }
} 

```


##***PLOC***Docker***PLOC***

***PLOC***Windows Server Containers can be managed with Docker commands.***PLOC***
***PLOC***While Windows containers should be comparable to their Linux counterparts and have the same management experience through Docker, there are some Docker commands that simply don't make sense with a Windows container.***PLOC***
***PLOC***Others simply haven't been tested (we're getting there).***PLOC***

***PLOC***In an effort to not duplicate the API documentation available in Docker, here is a link to their management APIs.***PLOC***
***PLOC***Their walkthroughs are fantastic.***PLOC***

***PLOC***We're tracking things that do and don't work in the Docker APIs in our Work in Progress document.***PLOC***


