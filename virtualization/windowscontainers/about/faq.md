***PLOC***ms.ContentId: F0D47E70-0BA1-4A06-B2F3-0232C496709D
title: Frequently asked questions***PLOC***

#***PLOC***Frequently Asked Questions***PLOC***

***PLOC***Last updated: May 1, 2015***PLOC***

##***PLOC***What is a Windows Server Container?***PLOC***

***PLOC***Windows Server Containers are a lightweight operating system virtualization method used to separate applications or services from other services running on the same container host.***PLOC***
***PLOC***To enable this, each container has its own view of the operating system, processes, file system, registry, and IP addresses.***PLOC***

##***PLOC***What is the difference between Linux and Windows Server Containers?***PLOC***

***PLOC***Linux and Windows Server Containers are similar -- both implement similar technologies within their kernel and core operating system.***PLOC***
***PLOC***The difference comes from the platform and workloads that run within the containers.***PLOC***
***PLOC***When a customer is using Windows Server Containers, they can integrate with existing Windows technologies such as .NET, ASP.NET, PowerShell and more.***PLOC***

##***PLOC***What is a Hyper-V Container?***PLOC***

***PLOC***You can think of a Hyper-V Container as a Windows Server Container running inside of a Hyper-V partition.***PLOC***

***PLOC***Hyper-V Containers offer an additional deployment option between the highly efficient, high-density Windows Server Container and the highly isolated hardware-virtualized Hyper-V virtual machine.***PLOC***
***PLOC***For environments where applications from different trust boundaries on the same host, additional isolation may be required.***PLOC***
***PLOC***Hyper-V Containers will provide higher isolation using an optimized virtualization and Windows Server operating system that separates containers from each other and from the host operating system.***PLOC***
***PLOC***Both container deployment options utilize the same management APIs, tools and image formats, at deployment time, customers can simply choose which deployment mode best meets their requirements.***PLOC***

##***PLOC***When will Hyper-V Containers be available for use?***PLOC***

***PLOC***We expect to deliver a preview of Hyper-V Containers this calendar year.***PLOC***

##***PLOC***Will Hyper-V Containers also be available to the Docker ecosystem?***PLOC***

***PLOC***Yes – Hyper-V Containers will provide the same level of integration and management with Docker as Windows Server Containers.***PLOC***
***PLOC***The goal is to have an open, consistent, cross-platform experience.***PLOC***
***PLOC***The Docker platform will also greatly simplify and enhance the experience of working across our container options.***PLOC***
***PLOC***An application developed using Windows Server Containers can be deployed as a Hyper-V Container without change.***PLOC***

##***PLOC***Why do I have to pick between Docker and PowerShell for Windows Server Container management?***PLOC***

*****PLOC***This isn't desired behavior nor our long term plan.***PLOC********PLOC***  PowerShell container management tools and Docker container management tools will work side by side in the future.***PLOC***

***PLOC***With that said, using multiple management interfaces to manage the same container can be difficult.***PLOC***

***PLOC***Take, for example, creating a container with PowerShell and naming the image with an upper case character.***PLOC***
***PLOC***Docker doesn’t support caps, PowerShell does.***PLOC***
***PLOC***While that specific example is very manageable, what gets much harder are handing state changes (race conditions and different expectations), feature set differences or versions…***PLOC***

***PLOC***Our short term decision was that management interfaces (in this case Docker and PowerShell) only see containers they created – you create a container with Docker and PowerShell doesn’t see it, you create it with PowerShell and Docker doesn’t see it.***PLOC***

##***PLOC***As a developer, do I have to re-write my app for each type of container?***PLOC***

***PLOC***No, Windows container images are common across both Windows Server Containers and Hyper-V Containers.***PLOC***
***PLOC***The choice of container type is made when you start the container.***PLOC***
***PLOC***From a developer standpoint, Windows Server Containers and Hyper-V Containers are two flavors of the same thing.***PLOC***
***PLOC***They offer the same development, programming and management experience, are open and extensible and will include the same level of integration and support via Docker.***PLOC***

***PLOC***A developer can create a container image using a Windows Server Container and deploy it as a Hyper-V Container or vice-versa without any changes other than specifying the appropriate runtime flag.***PLOC***

***PLOC***Windows Server Containers will offer greater density and performance (e.g. lower spin up time, faster runtime performance compared to nested configurations) for when speed is key.***PLOC***
***PLOC***Hyper-V Containers offer greater isolation, ensuring that code running in one container can't compromise or impact the host operating system or other containers running on the same host.***PLOC***
***PLOC***This is useful for multitenant scenarios (with requirements for hosting untrusted code) including SaaS applications and compute hosting.***PLOC***

##***PLOC***Are Hyper-V/Windows Server Containers an add-on, or will they integrated within Windows Server?***PLOC***

***PLOC***The container capabilities will be integrated into Windows Server 2016.***PLOC***
***PLOC***Stay tuned for more information closer to the general availability.***PLOC***

##***PLOC***What are the prerequisites for Windows Server Containers and Hyper-V Containers?***PLOC***

***PLOC***Both Window Server Containers and Hyper-V Containers require Windows Server 2016.***PLOC***
***PLOC***These technologies will not work with previous versions of Windows.***PLOC***

##***PLOC***Are Nano Server based containers supported?***PLOC***

***PLOC***For the TP3 release, no they are not.***PLOC***
***PLOC***Only Server Core based containers are currently supported.***PLOC***

##***PLOC***Can I run Windows Server Containers on ESXi or another non Hyper-V hypervisor?***PLOC***

***PLOC***Yes, Windows Server Container run on any TP3 Server Core installation.***PLOC***
***PLOC***Follow the instructions for ***PLOC***[***PLOC***enabling the containers feature in-place***PLOC***](../quick_start/inplace_setup.md)***PLOC***.***PLOC***

##***PLOC***Is Microsoft participating in the Open Container Initiative (OCI)?***PLOC***

***PLOC***To guarantee the packaging format remains universal, Docker recently organized the Open Container Initiative (OCI), aiming to ensure container packaging remains an open and foundation-led format with Microsoft as one of the founding members.***PLOC***

##***PLOC***Is Microsoft really partnering with Docker?***PLOC***

***PLOC***Yes.***PLOC***
***PLOC***Our partnership with Docker enables developers to create, manage and deploy both Windows Server and Linux containers using the same Docker tool set.***PLOC***
***PLOC***Developers targeting Windows Server will no longer have to make a choice between using the vast range of Windows Server technologies and building containerized applications.***PLOC***

***PLOC***Docker is two things, the open source group of projects and Docker the company.***PLOC***
***PLOC***We consider this partnership to include both.***PLOC***
***PLOC***Docker is successful, in part, because of the vibrant ecosystem that has built up around the Docker container technology.***PLOC***
***PLOC***Microsoft is contributing to the Docker Project, enabling support for Windows Server Containers and Hyper-V Containers.***PLOC***

***PLOC***For more information, see the ***PLOC***[***PLOC***New Windows Server containers and Azure support for Docker***PLOC***](http://azure.microsoft.com/blog/2014/10/15/new-windows-server-containers-and-azure-support-for-docker/?WT.mc_id=Blog_ServerCloud_Announce_TTD)***PLOC*** blog post.***PLOC***

-------------------
[Back to Container Home](../containers_welcome.md)


