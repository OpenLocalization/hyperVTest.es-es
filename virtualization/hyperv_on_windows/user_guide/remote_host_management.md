***PLOC***ms.ContentId: 7dcd6da0-dd72-422d-8752-5eccc8116e02
title: Managing remote Hyper-V hosts***PLOC***

#***PLOC***Manage Remote Hyper-V Hosts with Hyper-V Manager***PLOC***

***PLOC***Hyper-V Manager provides tools for diagnosing and managing your local Hyper-V host and a small number of remote hosts.***PLOC***
***PLOC***This article documents the configuration steps for connecting to Hyper-V hosts using Hyper-V Manager in all supported configurations.***PLOC***

***PLOC***To connect to a Hyper-V host in Hyper-V Manager, make sure ***PLOC********PLOC***Hyper-V Manager***PLOC********PLOC*** is selected in the left hand pane and then select ***PLOC********PLOC***Connect to Server...***PLOC********PLOC*** in the right-hand pane.***PLOC***

!(media/HyperVManager-ConnectToHost.png)

##***PLOC***Supported Hyper-V host combinations with Hyper-V Manager***PLOC***

***PLOC***Hyper-V Manager in Windows 10 allows you to manage:***PLOC***

*   ***PLOC***Windows 10***PLOC***
*   ***PLOC***Windows 8.1 and Windows Server 2012 R2 Hyper-V hosts***PLOC***
*   ***PLOC***Windows 8 and Windows 2012 Hyper-V hosts***PLOC***

***PLOC***Hyper-V Manager in Windows 8.1 and Windows Server 2012 R2 allows you to manage:***PLOC***

*   ***PLOC***Windows 8.1 and Windows Server 2012 R2 Hyper-V hosts***PLOC***
*   ***PLOC***Windows 8 and Windows 2012 Hyper-V hosts***PLOC***

> *****PLOC***Note:***PLOC********PLOC*** Not all Hyper-V Manager functionality works for all host versions.***PLOC***
> 

##***PLOC***Manage localhost***PLOC***

***PLOC***To add localhost to Hyper-V Manager as a Hyper-V host, select ***PLOC********PLOC***Local computer***PLOC********PLOC*** in the ***PLOC********PLOC***Select Computer***PLOC********PLOC*** dialogue box.***PLOC***

!(media/HyperVManager-ConnectToLocalHost.png)

***PLOC***If a connection can't be established:***PLOC***

*   ***PLOC***Make sure the Hyper-V server role is enabled.***PLOC***
    ***PLOC***See the ***PLOC***[***PLOC***walkthrough section for checking compatability***PLOC***](../quick_start/walkthrough_compatibility.md)***PLOC***.***PLOC***
*   ***PLOC***Confirm that your user account is part of the Hyper-V Administrator group.***PLOC***

##***PLOC***Manage a Hyper-V host in your domain***PLOC***

***PLOC***To add a remote Hyper-V host to Hyper-V Manager, select ***PLOC********PLOC***Another computer***PLOC********PLOC*** in the ***PLOC********PLOC***Select Computer***PLOC********PLOC*** dialogue box and enter the remote host's hostname, NetBIOS, or FQDN into the text field.***PLOC***

!(media/HyperVManager-ConnectToRemoteHost.png)

***PLOC***Windows 10 greatly expanded the possible combinations of remote connection types.***PLOC***
***PLOC***Now you can connect to a remote Windows 10 or later host using either the host name or IP address.***PLOC***
***PLOC***Hyper-V Manager now supports alternate credentials as well.***PLOC***

***PLOC***In order to manage remote Hyper-V hosts, remote management must be enabled on both computers.***PLOC***

***PLOC***You can do this through ***PLOC***`System Properties -> Remote Management Settings`***PLOC*** or by running the following PowerShell command as Administrator:  ***PLOC***

` PowerShell
winrm quickconfig
`

***PLOC***If your current user account matches a Hyper-V Administrator account on the remote host, go ahead and press ***PLOC********PLOC***OK***PLOC********PLOC*** to Connect.***PLOC***

***PLOC***This is the only supported way to manage a remote host in Hyper-V Manager in Windows 8 or Windows 8.1.***PLOC***

###***PLOC***Connect to the remote host as a different user***PLOC***

***PLOC***In Windows 10, if you are not running with the correct user account for the remote host, you can connect as another user with alternate credentials.***PLOC***

***PLOC***To specify credentials for the remote Hyper-V host, select ***PLOC********PLOC***Connect as another user: ** in the **Select Computer***PLOC********PLOC*** dialogue box then select ***PLOC********PLOC***Set User...***PLOC********PLOC***.***PLOC***

!(media/HyperVManager-ConnectToRemoteHostAltCreds.png)

> ***PLOC***Note:  It's very easy to forget to set the user and click OK with user not specified.***PLOC***
> ***PLOC***If your connection fails, make sure you actually did set the user.***PLOC***
> 

###***PLOC***Connect to the remote host using IP address***PLOC***

***PLOC***Sometimes it's easier to connect using IP address rather than host name.***PLOC***
***PLOC***Windows 10 allows your to do just that.***PLOC***

***PLOC***To connect using IP address, enter the IP address into the ***PLOC********PLOC***Another Computer***PLOC********PLOC*** text field.***PLOC***

##***PLOC***Manage a Hyper-V host outside your domain (or with no domain)***PLOC***

***PLOC***<!--Assuming this isn't done yet...again needs context.-->
Local Hyper-V Host:***PLOC***

1.  ***PLOC***Enable-PSRemoting
    Came back with netowork set to public.***PLOC***
    ***PLOC***Ran
    Set-NetConnectionProfile -Name "name" -NetworkCategory private***PLOC***
2.  ***PLOC***Set-Item WSMan:\localhost\Client\TrustedHosts * -Force***PLOC***
3.  ***PLOC***Enable-WSManCredSSP -Role client -DelegateComputer ****PLOC***

***PLOC***For workgroup only:***PLOC***

1.  ***PLOC***(should be done) Computer Policy\Administrative Templates\System\Credentials Delegation\Allow Delegating Fresh Credentials → Set to enabled and add WSMAN/* ].***PLOC***
    ***PLOC***To list of computers, check the box forConcatenate OS defaults with input above***PLOC***
2.  ***PLOC***Computer Policy\Administrative Templates\System\Credentials Delegation\Allow Delegating Fresh Credentials with NTLM-only server authentication → Set to enabled and add WSMAN/* to list of computers, check the box for Concatenate OS defaults with input above***PLOC***
3.  ***PLOC***Computer Policy\Administrative Templates\Windows Components\Windows Remote Management (WinRM)\WinRM Client\Allow CredSSP authentication → Set to enabled***PLOC***

***PLOC***Remote Hyper-V Host:***PLOC***

1.  ***PLOC***Disabled the firewall :)***PLOC***
2.  ***PLOC***Enable-PSRemoting***PLOC***
3.  ***PLOC***Set-Item WSMan:\localhost\Client\TrustedHosts * -Force
    So that's the demo-only instructions I used.***PLOC***
    ***PLOC***Replace * and turn off firewall with a single computer and letting credssp and winRM through***PLOC***


