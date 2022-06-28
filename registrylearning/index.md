# Windows Registry Learning

### The simple definition of windows registry
> The Windows Registry is a hierarchical database that stores low-level settings for the Microsoft Windows operating system and for applications that opt to use the registry. The kernel, device drivers, services, Security Accounts Manager, and user interfaces can all use the registry. 
> 
> Originally,When intruduced with win3.1,registry primarily stored configuration information for COM-based components. Windows 95 and Windows NT extended its use to rationalize and centralize the information in the profusion of INI files, which held the configurations for individual programs, and were stored at various locations.

>Like other files and services in Windows, all registry keys may be restricted by access control lists (ACLs), depending on user privileges, or on security tokens acquired by applications, or on system security policies enforced by the system (these restrictions may be predefined by the system itself, and configured by local system administrators or by domain administrators). Different users, programs, services or remote systems may only see some parts of the hierarchy or distinct hierarchies from the same root keys.

>https://en.wikipedia.org/wiki/Windows_Registry

Simply, registry is something contains windows's or programme's low-level configures and each registry entry has key and value.key is somthing like folder in windows file system and value is file in the innermost folder.Not all the applications need registry and different accesser who extra data from registry has different view which controled by local system administrators or by domain administrators.

Registry values are name/data pairs stored within keys,e.g.: 
>HKEY_CURRENT_USER\AppEvents\EventLabels\DeviceFail
![![20220628082955](httpscreepey-1306653668.cos.ap-shanghai.myqcloud.comnote20220628082955.png)](https://creepey-1306653668.cos.ap-shanghai.myqcloud.com/note/![20220628082955](httpscreepey-1306653668.cos.ap-shanghai.myqcloud.comnote20220628082955.png).png)
*Each registry value stored in a registry key has a unique name whose letter case is not significant！*
### Details of seven predefined root keys

#### HKEY_LOCAL_MACHINE (HKLM)


#### HKEY_CLASSES_ROOT (HKCR)

#### HKEY_USERS (HKU)

#### HKEY_CURRENT_USER (HKCU)

#### HKEY_PERFORMANCE_DATA

#### HKEY_DYN_DATA

