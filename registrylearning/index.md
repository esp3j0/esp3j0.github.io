# Windows Registry Learning

## The simple definition of windows registry
> The Windows Registry is a hierarchical database that stores low-level settings for the Microsoft Windows operating system and for applications that opt to use the registry. The kernel, device drivers, services, Security Accounts Manager, and user interfaces can all use the registry. 
> 
> Originally,When intruduced with win3.1,registry primarily stored configuration information for COM-based components. Windows 95 and Windows NT extended its use to rationalize and centralize the information in the profusion of INI files, which held the configurations for individual programs, and were stored at various locations.

>Like other files and services in Windows, all registry keys may be restricted by access control lists (ACLs), depending on user privileges, or on security tokens acquired by applications, or on system security policies enforced by the system (these restrictions may be predefined by the system itself, and configured by local system administrators or by domain administrators). Different users, programs, services or remote systems may only see some parts of the hierarchy or distinct hierarchies from the same root keys.

>https://en.wikipedia.org/wiki/Windows_Registry

Simply, registry is something contains windows's or programme's low-level configures and each registry entry has key and value.key is somthing like folder in windows file system and value is file in the folder.Not all the applications need registry and different accesser who extra data from registry has different view that controled by local system administrators or by domain administrators.

Registry values are name/data pairs stored within keys,e.g.: 
>HKEY_CURRENT_USER\AppEvents\EventLabels\DeviceFail
![![20220628082955](httpscreepey-1306653668.cos.ap-shanghai.myqcloud.comnote20220628082955.png)](https://creepey-1306653668.cos.ap-shanghai.myqcloud.com/note/![20220628082955](httpscreepey-1306653668.cos.ap-shanghai.myqcloud.comnote20220628082955.png).png)

*Each registry value stored in a registry key has a unique name whose letter case is not significant！*

## registry value type
> Before studying predefined root keys,let's learn more about value's type.

|type id|type name|meaning and encoding
|---|---|---
|0|REG_NONE|No type (the stored value, if any)
|1|REG_SZ|A string value, normally stored and exposed in UTF-16LE (when using the Unicode version of Win32 API functions), usually terminated by a NUL character
|2|An "expandable" string value that can contain environment variables, normally stored and exposed in UTF-16LE, usually terminated by a NUL character
|3|REG_BINARY|Binary data (any arbitrary data)
|4|REG_DWORD / REG_DWORD_LITTLE_ENDIAN|A DWORD value, a 32-bit unsigned integer (numbers between 0 and 4,294,967,295 [232 – 1]) (little-endian)
|5|REG_DWORD_BIG_ENDIAN|A DWORD value, a 32-bit unsigned integer (numbers between 0 and 4,294,967,295 [232 – 1]) (big-endian)
|6|REG_LINK|A symbolic link (UNICODE) to another registry key, specifying a root key and the path to the target key
|7|REG_MULTI_SZ|A multi-string value, which is an ordered list of non-empty strings, normally stored and exposed in Unicode, each one terminated by a null character, the list being normally terminated by a second null character.
|8|REG_RESOURCE_LIST|A resource list (used by the Plug-n-Play hardware enumeration and configuration)
|9|REG_FULL_RESOURCE_DESCRIPTOR|A resource descriptor (used by the Plug-n-Play hardware enumeration and configuration)
|10|REG_RESOURCE_REQUIREMENTS_LIST|A resource requirements list (used by the Plug-n-Play hardware enumeration and configuration)
|11|REG_QWORD / REG_QWORD_LITTLE_ENDIAN|A QWORD value, a 64-bit integer (either big- or little-endian, or unspecified) (introduced in Windows 2000)


## Details of seven predefined root keys

### HKEY_LOCAL_MACHINE (HKLM)

#### summary of  HKLM
> Abbreviated HKLM, HKEY_LOCAL_MACHINE stores settings that are specific to the local computer.The key located by HKLM is actually not stored on disk, but maintained in memory by the system kernel in order to map all the other subkeys. In the windows nt era，HKLM contains four subkeys, "SAM", "SECURITY", "SYSTEM", and "SOFTWARE" that are loaded at boot time within their respective files located in the %SystemRoot%\System32\config folder.  A fifth subkey, "HARDWARE", is volatile and is created dynamically, and as such is not stored in a file (it exposes a view of all the currently detected Plug-and-Play devices). On Windows Vista and above, a sixth and seventh subkey, "COMPONENTS" and "BCD", are mapped in memory by the kernel on-demand and loaded from %SystemRoot%\system32\config\COMPONENTS or from boot configuration data, \boot\BCD on the system partition.

#### HKLM\SAM
The "HKLM\SAM" key usually appears as empty for most users (unless they are granted access by administrators of the local system or administrators of domains managing the local system). It is used to reference all "Security Accounts Manager" (SAM) databases for all domains into which the local system has been administratively authorized or configured (including the local domain of the running system, whose SAM database is stored in a subkey also named "SAM": other subkeys will be created as needed, one for each supplementary domain). Each SAM database contains all builtin accounts (mostly group aliases) and configured accounts (users, groups and their aliases, including guest accounts and administrator accounts) created and configured on the respective domain, for each account in that domain, it notably contains the user name which can be used to log on that domain, the internal unique user identifier in the domain, a cryptographic hash of each user's password for each enabled authentication protocol, the location of storage of their user registry hive, various status flags (for example if the account can be enumerated and be visible in the logon prompt screen), and the list of domains (including the local domain) into which the account was configured.


#### HKLM\SECURITY
The "HKLM\SECURITY" key usually appears empty for most users (unless they are granted access by users with administrative privileges) and is linked to the Security database of the domain into which the current user is logged on (if the user is logged on the local system domain, this key will be linked to the registry hive stored by the local machine and managed by local system administrators or by the builtin "System" account and Windows installers). The kernel will access it to read and enforce the security policy applicable to the current user and all applications or operations executed by this user. It also contains a "SAM" subkey which is dynamically linked to the SAM database of the domain onto which the current user is logged on.

#### HKLM\SYSTEM
User with administrative privileges can write this key. It contains information about the Windows system setup, data for the secure random number generator (RNG), the list of currently mounted devices containing a filesystem, several numbered "HKLM\SYSTEM\Control Sets" containing alternative configurations for system hardware drivers and services running on the local system (including the currently used one and a backup), a "HKLM\SYSTEM\Select" subkey containing the status of these Control Sets, and a "HKLM\SYSTEM\CurrentControlSet" which is dynamically linked at boot time to the Control Set which is currently used on the local system. Each configured Control Set contains:
- an "Enum" subkey enumerating all known Plug-and-Play devices and associating them with installed system drivers (and storing the device-specific configurations of these drivers),
- a "Services" subkey listing all installed system drivers (with non device-specific configuration, and the enumeration of devices for which they are instantiated) and all programs running as services (how and when they can be automatically started),
- a "Control" subkey organizing the various hardware drivers and programs running as services and all other system-wide configuration,
- a "Hardware Profiles" subkey enumerating the various profiles that have been tuned (each one with "System" or "Software" settings used to modify the default profile, either in system drivers and services or in the applications) as well as the "Hardware Profiles\Current" subkey which is dynamically linked to one of these profiles.

#### HKLM\SOFTWARE
its subkey contains software and Windows settings (in the default hardware profile). It is mostly modified by application and system installers. It is organized by software vendor (with a subkey for each), but also contains a "Windows" subkey for some settings of the Windows user interface, a "Classes" subkey containing all registered associations from file extensions, MIME types, Object Classes IDs and interfaces IDs (for OLE, COM/DCOM and ActiveX), to the installed applications or DLLs that may be handling these types on the local machine (however these associations are configurable for each user, see below), and a "Policies" subkey (also organized by vendor) for enforcing general usage policies on applications and system services (including the central certificates store used for authenticating, authorizing or disallowing remote systems or services running outside the local network domain).
The "HKLM\SOFTWARE\Wow6432Node" key is used by 32-bit applications on a 64-bit Windows OS, and is equivalent to but separate from "HKLM\SOFTWARE". The key path is transparently presented to 32-bit applications by WoW64 as HKLM\SOFTWARE(in a similar way that 32-bit applications see %SystemRoot%\Syswow64 as %SystemRoot%\System32)
### HKEY_CLASSES_ROOT (HKCR)
Abbreviated HKCR, HKEY_CLASSES_ROOT contains information about registered applications, such as file associations and OLE Object Class IDs, tying them to the applications used to handle these items. On Windows 2000 and above, HKCR is a compilation of user-based HKCU\Software\Classes and machine-based HKLM\Software\Classes. If a given value exists in both of the subkeys above, the one in HKCU\Software\Classes takes precedence.The design allows for either machine- or user-specific registration of COM objects.
### HKEY_USERS (HKU)
Abbreviated HKU, HKEY_USERS contains subkeys corresponding to the HKEY_CURRENT_USER keys for each user profile actively loaded on the machine, though user hives are usually only loaded for currently logged-in users.
### HKEY_CURRENT_USER (HKCU)
Abbreviated HKCU, HKEY_CURRENT_USER stores settings that are specific to the currently logged-in user. The HKEY_CURRENT_USER key is a link to the subkey of HKEY_USERS that corresponds to the user; the same information is accessible in both locations. The specific subkey referenced is "(HKU)\(SID)\..." where (SID) corresponds to the Windows SID; if the "(HKCU)" key has the following suffix "(HKCU)\Software\Classes\..." then it corresponds to "(HKU)\(SID)_CLASSES\..." i.e. the suffix has the string "_CLASSES" is appended to the (SID).
On Windows NT systems, each user's settings are stored in their own files called NTUSER.DAT and USRCLASS.DAT inside their own Documents and Settings subfolder (or their own Users sub folder in Windows Vista and above). Settings in this hive follow users with a roaming profile from machine to machine.
### HKEY_PERFORMANCE_DATA (only in Windows NT, but invisible in the Windows Registry Editor)
This key provides runtime information into performance data provided by either the NT kernel itself, or running system drivers, programs and services that provide performance data. This key is not stored in any hive and not displayed in the Registry Editor, but it is visible through the registry functions in the Windows API, or in a simplified view via the Performance tab of the Task Manager (only for a few performance data on the local system) or via more advanced control panels (such as the Performances Monitor or the Performances Analyzer which allows collecting and logging these data, including from remote systems).
### HKEY_DYN_DATA  (only in Windows 9x, and visible in the Windows Registry Editor)
This key is used only on Windows 95, Windows 98 and Windows ME. It contains information about hardware devices, including Plug and Play and network performance statistics. The information in this hive is also not stored on the hard drive. The Plug and Play information is gathered and configured at startup and is stored in memory.

