***PLOC***ms.ContentId: 8DE9250B-556B-47BC-AD9A-8992B3D3D0F9
title: PowerShell Snippets***PLOC***

#***PLOC***PowerShell Snippets***PLOC***

***PLOC***PowerShell is an awesome scripting, automation, and management tool for Hyper-V.  Here is a toolbox for exploring some of the cool things it can do!***PLOC***

***PLOC***All Hyper-V management requires running as administrator so assume all scripts and snippets must be run as administrator from a Hyper-V Administrator account.***PLOC***

***PLOC***If you aren't sure if you have the right permissions, type ***PLOC***`Get-VM`***PLOC*** and if it runs with no errors, you're ready to go.***PLOC***

##***PLOC***PowerShell Direct tools***PLOC***

***PLOC***All of the scripts and snippets in this section will rely on the following basics.***PLOC***

*****PLOC***Requirements***PLOC********PLOC*** :  ***PLOC***

*   ***PLOC***PowerShell Direct.***PLOC***
    ***PLOC***Windows 10 guest and host OS.***PLOC***

*****PLOC***Common Variables***PLOC********PLOC*** :  
***PLOC***`$VMName`***PLOC*** -- this is a string with the VMName.***PLOC***
***PLOC***See a list of available VMs with ***PLOC***`Get-VM``$cred`***PLOC*** -- Credential for the guest OS.***PLOC***
***PLOC***Can be populated using ***PLOC***`$cred = Get-Credential`

###***PLOC***Check if the guest has booted***PLOC***

***PLOC***Hyper-V Manager doesn't give you visibility into the guest operating system which often makes it difficult to know whether the guest OS has booted.***PLOC***

***PLOC***Use this command to check whether the guest has booted.***PLOC***

***PLOC***``` PowerShell
if((Invoke-Command -VMName $VMName -Credential $cred {"Test"}) -ne "Test"){Write-Host "Not Booted"} else {Write-Host "Booted"}***PLOC***


```

**Outcome**  
Prints a friendly message declaring the state of the guest OS.


### Script locking until the guest has booted

The following function waits uses the same principle to wait until PowerShell is available in the guest (meaning the OS has booted and most services are running) then returns.

``` PowerShell
function waitForPSDirect([string]$VMName, $cred){
   Write-Output "[$($VMName)]:: Waiting for PowerShell Direct (using $($cred.username))"
   while ((Invoke-Command -VMName $VMName -Credential $cred {"Test"} -ea SilentlyContinue) -ne "Test") {Sleep -Seconds 1}}

```

*****PLOC***Outcome***PLOC********PLOC***  
Prints a friendly message and locks until the connection to the VM succeeds.***PLOC***
***PLOC***Succeeds silently.***PLOC***

###***PLOC***Script locking until the guest has a network***PLOC***

***PLOC***With PowerShell Direct it is possible to get connected to a PowerShell session inside a virtual machine before the virtual machine has received an IP address.***PLOC***

***PLOC***``` PowerShell***PLOC***

#***PLOC***Wait for DHCP***PLOC***

***PLOC***while ((Get-NetIPAddress | ?***PLOC***
***PLOC***AddressFamily -eq IPv4 | ?***PLOC***
***PLOC***IPAddress -ne 127.0.0.1).SuffixOrigin -ne "Dhcp") {sleep -Milliseconds 10}
```***PLOC***

****PLOC**** Outcome ****PLOC*******PLOC***
Locks until a DHCP lease is recieved.***PLOC***
***PLOC***Since this script is not looking for a specific subnet or IP address, it works no matter what network configuration you're using.***PLOC***
***PLOC***Succeeds silently.***PLOC***

##***PLOC***Managing credentials with PowerShell***PLOC***

***PLOC***Hyper-V scripts frequently require handling credentials for one or more virtual machines, Hyper-V host, or both.***PLOC***

***PLOC***There are multiple ways you can achieve this when working with PowerShell Direct or standard PowerShell remoting:***PLOC***

1.  ***PLOC***The first (and simplest) way is to have the same user credentials be valid in the host and the guest or local and remote host.***PLOC***
    ***PLOC***This is quite easy if you are logging in with your Microsoft account - or if you are in a domain environment.***PLOC***
    ***PLOC***In this scenario you can just run ***PLOC***`Invoke-Command -VMName "test" {get-process}`***PLOC***.***PLOC***
2.  ***PLOC***Let PowerShell prompt you for credentials  
    If your credentials do not match you will automatically get a credential prompt allowing you to provide the appropriate credentials for the virtual machine.***PLOC***
3.  ***PLOC***Store credentials in a variable for reuse.***PLOC***
    ***PLOC***Running a simple command like this:  
    ***PLOC***` PowerShell
    $localCred = Get-Credential
    `***PLOC***
    And then running something like this:
    ``` PowerShell
    Invoke-Command -VMName "test" -Credential $localCred  {get-process}***PLOC***


  ```
  Will mean that you only get prompted once per script/PowerShell session for your credentials.

4. Code your credentials into your scripts.  **Don't do this for any real workload or system**
 > Warning:  _Do not do this in a production system.  Do not do this with real passwords._

  You can hand craft a PSCredential object with some code like this:  
  ``` PowerShell
  $localCred = New-Object -typename System.Management.Automation.PSCredential -argumentlist "Administrator", (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force) 

  ```

***PLOC***Grossly insecure - but useful for testing.***PLOC***
***PLOC***Now you get no prompts at all in this session.***PLOC***


