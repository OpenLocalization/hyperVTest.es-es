***PLOC***ms.ContentId: 95FE9554-3968-4EED-B65D-E03F06A7598D
title: Step 3: Create a virtual switch***PLOC***

#***PLOC***Step 3: Create a virtual switch***PLOC***

***PLOC***A virtual switch allows you to create a network connection for your virtual machine.***PLOC***
***PLOC***They are used just like the network adapter (NIC) on your physical computer.***PLOC***

***PLOC***For this example, we are going to create an External switch.***PLOC***
***PLOC***The external switch will allow your virtual machine to access the host machine's network adapter.***PLOC***
***PLOC***If your host machine is connected to the internet, your virtual machine will be as well.***PLOC***

***PLOC***We'll also set the switch to allow the host to share this network adapter.***PLOC***
***PLOC***This makes it so both the virtual machines and the host can use the same network.***PLOC***


1.  ***PLOC***In Hyper-V manager, click ***PLOC********PLOC***Virtual Switch Manager***PLOC********PLOC***.***PLOC***
    
    !(media/virtual_switch_manager1.png)
2.  ***PLOC***Select ***PLOC********PLOC***New virtual network switch***PLOC********PLOC***.***PLOC***
    
    !(media/new_switch.png)
3.  ***PLOC***Select ***PLOC********PLOC***External***PLOC********PLOC*** and ***PLOC********PLOC***Create Virtual Switch***PLOC********PLOC***.***PLOC***
    
    !(media/new_switch_createbutton.png)
4.  ***PLOC***Under ***PLOC********PLOC***Name***PLOC********PLOC***, type ***PLOC********PLOC***External***PLOC********PLOC***.***PLOC***
5.  ***PLOC***Under ***PLOC********PLOC***External network***PLOC********PLOC***, select the correct network adapter (there will probably only be one option).***PLOC***
6.  ***PLOC***Select ***PLOC********PLOC***Allow management operating system to share this network adapter***PLOC********PLOC*** and click ***PLOC********PLOC***OK***PLOC********PLOC***.***PLOC***
    
    !(media/share_nic.png)
7.  ***PLOC***You'll get a message warning you that your network might disconnect while the virtual switch is created.***PLOC***
    ***PLOC***Just click ***PLOC********PLOC***Yes***PLOC********PLOC***.***PLOC***
    ***PLOC***Your network will be unavailable for a short time.***PLOC***
    
    !(media/network_warning.png)

##***PLOC***Next step:***PLOC***

[***PLOC***Step 4: Create a Windows virtual machine from an .iso file***PLOC***](walkthrough_create_vm.md)


