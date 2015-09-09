***PLOC***ms.ContentId: 3fdd690d-4259-4066-8781-360bb0554512
title: Running Apps in Windows Containers***PLOC***

#***PLOC***Application Compatability in Windows Server Containers***PLOC***

***PLOC***Is something not on this list?***PLOC***
***PLOC***Let us know what fails and succeeds in your environment via ***PLOC***[***PLOC***the forums***PLOC***](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)***PLOC***.***PLOC***

##***PLOC***Which applications run in a Windows Server Container***PLOC***

***PLOC***We have tried to running the following applications in a Windows Server Container.***PLOC***
***PLOC***These results do not guarantee that the application is working.***PLOC***
***PLOC***The sole purpose is to share our experience.***PLOC***

| *****PLOC***Name***PLOC*****| *****PLOC***Version***PLOC*****| *****PLOC***Does it work?***PLOC*****| *****PLOC***Comment***PLOC*****|
|:-----|:-----|:-----|:-----|
| ***PLOC***.NET***PLOC***| ***PLOC***3.5***PLOC***| ***PLOC***No***PLOC***| ***PLOC***Fails to install properly***PLOC***|
| ***PLOC***.NET***PLOC***| ***PLOC***4.6***PLOC***| ***PLOC***Yes***PLOC***| ***PLOC***Included in base image***PLOC***|
| ***PLOC***.NET CLR***PLOC***| ***PLOC***5 beta 6***PLOC***| ***PLOC***Yes***PLOC***| ***PLOC***Both, x64 and x86***PLOC***|
| ***PLOC***Active Python***PLOC***| ***PLOC***3.4.1***PLOC***| ***PLOC***Yes***PLOC***| |
| ***PLOC***Apache CouchDB***PLOC***| ***PLOC***1.6.1***PLOC***| ***PLOC***No***PLOC***| |
| ***PLOC***Apache HTTPD***PLOC***| ***PLOC***2.4***PLOC***| ***PLOC***Yes***PLOC***| |
| ***PLOC***Apache Tomcat***PLOC***| ***PLOC***8.0.24 x64***PLOC***| ***PLOC***Yes***PLOC***| |
| ***PLOC***ASP.NET***PLOC***| ***PLOC***3.5***PLOC***| ***PLOC***No***PLOC***| |
| ***PLOC***ASP.NET***PLOC***| ***PLOC***4.5***PLOC***| ***PLOC***No***PLOC***| |
| ***PLOC***ASP.NET***PLOC***| ***PLOC***5 beta 6***PLOC***| ***PLOC***Yes***PLOC***| ***PLOC***Both, x64 and x86***PLOC***|
| ***PLOC***Erlang/OTP***PLOC***| ***PLOC***18.0***PLOC***| ***PLOC***No***PLOC***| |
| ***PLOC***FileZilla FTP Server***PLOC***| ***PLOC***0.9***PLOC***| ***PLOC***Yes***PLOC***| ***PLOC***Has to be installed through an RDP session  into the container***PLOC***|
| ***PLOC***Go Progamming Language***PLOC***| ***PLOC***1.4.2***PLOC***| ***PLOC***Yes***PLOC***| |
| ***PLOC***Internet Information Service***PLOC***| ***PLOC***10.0***PLOC***| ***PLOC***Yes***PLOC***| |
| ***PLOC***Java***PLOC***| ***PLOC***1.8.0_51***PLOC***| ***PLOC***Yes***PLOC***| ***PLOC***Use the server version.***PLOC******PLOC***The client version does not install properly***PLOC***|
| ***PLOC***Jetty***PLOC***| ***PLOC***9.3***PLOC***| ***PLOC***Partially***PLOC***| ***PLOC***Running demo-base fails***PLOC***|
| ***PLOC***MineCraft Server***PLOC***| ***PLOC***1.8.5***PLOC***| ***PLOC***Yes***PLOC***| |
| ***PLOC***MongoDB***PLOC***| ***PLOC***3.0.4***PLOC***| ***PLOC***Yes***PLOC***| |
| ***PLOC***MySQL***PLOC***| ***PLOC***5.6.26***PLOC***| ***PLOC***Yes***PLOC***| |
| ***PLOC***NGinx***PLOC***| ***PLOC***1.9.3***PLOC***| ***PLOC***Yes***PLOC***| |
| ***PLOC***Node.js***PLOC***| ***PLOC***0.12.6***PLOC***| ***PLOC***Partially***PLOC***| ***PLOC***Running node with js files works.***PLOC******PLOC***NPM fails to download packages.***PLOC******PLOC***Running node interactively does not work properly.***PLOC***|
| ***PLOC***PHP***PLOC***| ***PLOC***5.6.11***PLOC***| ***PLOC***Partially***PLOC***| ***PLOC***With Apache, IIS via FastCGI currently does not work.***PLOC***|
| ***PLOC***PostgreSQL***PLOC***| ***PLOC***9.4.4***PLOC***| ***PLOC***Yes***PLOC***| |
| ***PLOC***Python***PLOC***| ***PLOC***3.4.3***PLOC***| ***PLOC***Yes***PLOC***| |
| ***PLOC***R***PLOC***| ***PLOC***3.2.1***PLOC***| ***PLOC***No***PLOC***| |
| ***PLOC***RabbitMQ***PLOC***| ***PLOC***3.5.x***PLOC***| ***PLOC***Yes***PLOC***| ***PLOC***Has to be installed through an RDP session  into the container***PLOC***|
| ***PLOC***Redis***PLOC***| ***PLOC***2.8.2101***PLOC***| ***PLOC***Yes***PLOC***| |
| ***PLOC***Ruby***PLOC***| ***PLOC***2.2.2***PLOC***| ***PLOC***Yes***PLOC***| ***PLOC***Both, x64 and x86***PLOC***|
| ***PLOC***Ruby on Rails***PLOC***| ***PLOC***4.2.3***PLOC***| ***PLOC***Yes***PLOC***| |
| ***PLOC***SQLite***PLOC***| ***PLOC***3.8.11.1***PLOC***| ***PLOC***Yes***PLOC***| |
| ***PLOC***SQL Server Express***PLOC***| ***PLOC***2014 LocalDB***PLOC***| ***PLOC***No***PLOC***| |
| ***PLOC***Sysinternals Tools***PLOC***| ***PLOC*******PLOC***| ***PLOC***Yes***PLOC***| ***PLOC***Only tried those not requiring a GUI.***PLOC******PLOC***PsExec does not work by current design***PLOC***|

##***PLOC***What Optional Windows Features can I install?***PLOC***

***PLOC***The following Windows Optional Features have been confirmed as being able to install.***PLOC***
***PLOC***Many do not function once they are installed at this point in time.***PLOC***

*   ***PLOC***AD-Certificate***PLOC***
*   ***PLOC***ADCS-Cert-Authority***PLOC***
*   ***PLOC***File-Services***PLOC***
    
    *   ***PLOC***FS-FileServer***PLOC***
    *   ***PLOC***FS-VSS-Agent***PLOC***
*   ***PLOC***DirectAccess-VPN***PLOC***
*   ***PLOC***Routing***PLOC***
*   ***PLOC***Remote-Desktop-Services***PLOC***
*   ***PLOC***VolumeActivation***PLOC***
*   ***PLOC***Web-Server***PLOC***
*   ***PLOC***Web-WebServer***PLOC***
*   ***PLOC***Web-Common-Http***PLOC***
*   ***PLOC***Web-Default-Doc***PLOC***
*   ***PLOC***Web-Dir-Browsing***PLOC***
*   ***PLOC***Web-Http-Errors***PLOC***
*   ***PLOC***Web-Static-Content***PLOC***
*   ***PLOC***Web-Http-Redirect***PLOC***
*   ***PLOC***Web-DAV-Publishing***PLOC***
*   ***PLOC***Web-Health***PLOC***
*   ***PLOC***Web-Http-Logging***PLOC***
*   ***PLOC***Web-Custom-Logging***PLOC***
*   ***PLOC***Web-Log-Libraries***PLOC***
*   ***PLOC***Web-ODBC-Logging***PLOC***
*   ***PLOC***Web-Request-Monitor***PLOC***
*   ***PLOC***Web-Performance***PLOC***
*   ***PLOC***Web-Stat-Compression***PLOC***
*   ***PLOC***Web-Dyn-Compression***PLOC***
*   ***PLOC***Web-Security***PLOC***
*   ***PLOC***Web-Filtering***PLOC***
*   ***PLOC***Web-Basic-Auth***PLOC***
*   ***PLOC***Web-CertProvider***PLOC***
*   ***PLOC***Web-Client-Auth***PLOC***
*   ***PLOC***Web-Digest-Auth***PLOC***
*   ***PLOC***Web-Cert-Auth***PLOC***
*   ***PLOC***Web-IP-Security***PLOC***
*   ***PLOC***Web-Url-Auth***PLOC***
*   ***PLOC***Web-Windows-Auth***PLOC***
*   ***PLOC***Web-App-Dev***PLOC***
*   ***PLOC***Web-AppInit***PLOC***
*   ***PLOC***Web-CGI***PLOC***
*   ***PLOC***Web-ISAPI-Ext***PLOC***
*   ***PLOC***Web-ISAPI-Filter***PLOC***
*   ***PLOC***Web-Includes***PLOC***
*   ***PLOC***Web-WebSockets***PLOC***
*   ***PLOC***Web-Mgmt-Compat***PLOC***
*   ***PLOC***Web-Metabase***PLOC***
*   ***PLOC***BitLocker***PLOC***
*   ***PLOC***EnhancedStorage***PLOC***
*   ***PLOC***GPMC***PLOC***
*   ***PLOC***Isolated-UserMode***PLOC***
*   ***PLOC***Server-Media-Foundation***PLOC***
*   ***PLOC***MSMQ-DCOM***PLOC***
*   ***PLOC***MultiPoint-Connector-Feature***PLOC***
*   ***PLOC***qWave***PLOC***
*   ***PLOC***RDC***PLOC***
*   ***PLOC***RSAT-Feature-Tools-BitLocker***PLOC***
*   ***PLOC***RSAT-Clustering-PowerShell***PLOC***
*   ***PLOC***RSAT-Clustering-AutomationServer***PLOC***
*   ***PLOC***RSAT-Clustering-CmdInterface***PLOC***
*   ***PLOC***RSAT-Shielded-VM-Tools***PLOC***
*   ***PLOC***RSAT-AD-Tools***PLOC***
*   ***PLOC***RSAT-AD-PowerShell***PLOC***
*   ***PLOC***RSAT-ADDS***PLOC***
*   ***PLOC***RSAT-AD-AdminCenter***PLOC***
*   ***PLOC***RSAT-ADDS-Tools***PLOC***
*   ***PLOC***RSAT-ADLDS***PLOC***
*   ***PLOC***Hyper-V-PowerShell***PLOC***
*   ***PLOC***UpdateServices-API***PLOC***
*   ***PLOC***RSAT-NetworkController***PLOC***
*   ***PLOC***Windows-Fabric-Tools***PLOC***
*   ***PLOC***RSAT-HostGuardianService***PLOC***
*   ***PLOC***FS-SMBBW***PLOC***
*   ***PLOC***Storage-Replica***PLOC***
*   ***PLOC***Telnet-Client***PLOC***
*   ***PLOC***WAS***PLOC***
    
    *   ***PLOC***WAS-Process-Model***PLOC***
    *   ***PLOC***WAS-Config-APIs***PLOC***
*   ***PLOC***Windows-Server-Backup***PLOC***
*   ***PLOC***Migration***PLOC***

***PLOC***Is something not on this list?***PLOC***
***PLOC***Let us know what fails and succeeds in your environment via ***PLOC***[***PLOC***the forums***PLOC***](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers)***PLOC***.***PLOC***


