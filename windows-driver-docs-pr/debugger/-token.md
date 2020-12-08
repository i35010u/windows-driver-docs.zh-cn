---
title: 令牌
description: 标记扩展显示安全令牌对象的格式化视图。
keywords:
- 令牌
- 安全令牌
- 令牌 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- token
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 244bd4391907be201c5f75ab9a302ae687e45b67
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803283"
---
# <a name="token"></a>!token


**！令牌** 扩展显示安全令牌对象的格式化视图。

Kernel-Mode 语法：

```dbgcmd
!token [-n] [Address] 
!token -?
```

User-Mode 语法：

```dbgcmd
!token [-n] [Handle] 
!token -?
```

## <a name="span-idddk__token_dbgspanspan-idddk__token_dbgspanparameters"></a><span id="ddk__token_dbg"></span><span id="DDK__TOKEN_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
仅 (内核模式) 指定要显示的令牌的地址。 如果此为0或省略，则显示活动线程的标记。

<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*句柄*   
 (用户模式仅) 指定要显示的令牌的句柄。 如果此为0或省略，则显示与目标线程关联的标记。

<span id="_______-n______"></span><span id="_______-N______"></span>**-n**   
 (用户模式仅) 导致显示包含友好名称。 这包括 sid) 类型 (安全标识符，以及 SID 的域和用户名。 调试 LSASS 时不能使用此选项。

<span id="_______-_______"></span> **-?**   
显示此扩展的帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Exts.dll

在内核模式和实时用户模式调试中可以使用 **！ token** 命令。 它不能用于用户模式转储文件。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关内核模式令牌结构的详细信息，请参阅 Russinovich 和 David 所罗门群岛的 *Microsoft Windows 内部机制* 。 有关用户模式令牌结构的信息，请参阅 Microsoft Windows SDK 文档。

<a name="remarks"></a>备注
-------

令牌结构是表示已进行身份验证的用户进程的安全对象类型。 每个进程都具有分配的标记，该标记将成为该进程的每个线程的默认标记。 但是，可以为单个线程分配一个重写此默认值的令牌。

可以从 [**！进程**](-process.md)的输出中获取令牌地址。 若要显示令牌结构的各个字段的列表，请使用 **dt nt！ \_标记** 命令。

以下是示例：

```dbgcmd
kd> !process 81464da8 1
PROCESS 81464da8  SessionId: 0  Cid: 03bc    Peb: 7ffdf000  ParentCid: 0124
    DirBase: 0dec2000  ObjectTable: e1a31198  TableSize: 275.
    Image: MSMSGS.EXE
    VadRoot 81468cc0 Vads 170 Clone 0 Private 455. Modified 413. Locked 0.
    DeviceMap e1958438
    Token                             e1bed030
    ElapsedTime                       0:44:15.0142
    UserTime                          0:00:00.0290
    KernelTime                        0:00:00.0300
    QuotaPoolUsage[PagedPool]         49552
    QuotaPoolUsage[NonPagedPool]      10872
    Working Set Sizes (now,min,max)  (781, 50, 345) (3124KB, 200KB, 1380KB)
    PeakWorkingSetSize                1550
    VirtualSize                       57 Mb
    PeakVirtualSize                   57 Mb
    PageFaultCount                    2481
    MemoryPriority                    BACKGROUND
    BasePriority                      8
    CommitCharge                      2497
kd> !exts.token -n e1bed030
_TOKEN e1bed030
TS Session ID: 0
User: S-1-5-21-518066528-515770016-299552555-2981724 (User: MYDOMAIN\myuser)
Groups:
 00 S-1-5-21-518066528-515770016-299552555-513 (Group: MYDOMAIN\Domain Users)
    Attributes - Mandatory Default Enabled
 01 S-1-1-0 (Well Known Group: localhost\Everyone)
    Attributes - Mandatory Default Enabled
 02 S-1-5-32-544 (Alias: BUILTIN\Administrators)
    Attributes - Mandatory Default Enabled Owner
 03 S-1-5-32-545 (Alias: BUILTIN\Users)
    Attributes - Mandatory Default Enabled
 04 S-1-5-21-518066528-515770016-299552555-2999049 (Group: MYDOMAIN\AllUsers)
    Attributes - Mandatory Default Enabled
 05 S-1-5-21-518066528-515770016-299552555-2931095 (Group: MYDOMAIN\SomeGroup1)
    Attributes - Mandatory Default Enabled
 06 S-1-5-21-518066528-515770016-299552555-2931096 (Group: MYDOMAIN\SomeGroup2)
    Attributes - Mandatory Default Enabled
 07 S-1-5-21-518066528-515770016-299552555-3014318 (Group: MYDOMAIN\SomeGroup3)
    Attributes - Mandatory Default Enabled
 08 S-1-5-21-518066528-515770016-299552555-3053352 (Group: MYDOMAIN\Another Group)
    Attributes - Mandatory Default Enabled
 09 S-1-5-21-518066528-515770016-299552555-2966661 (Group: MYDOMAIN\TestGroup)
    Attributes - Mandatory Default Enabled
 10 S-1-5-21-2117033040-537160606-1609722162-17637 (Group: MYOTHERDOMAIN\someusers)
    Attributes - Mandatory Default Enabled
 11 S-1-5-21-518066528-515770016-299552555-3018354 (Group: MYDOMAIN\TestGroup2)
    Attributes - Mandatory Default Enabled
 12 S-1-5-21-518066528-515770016-299552555-3026602 (Group: MYDOMAIN\SomeGroup4)
    Attributes - Mandatory Default Enabled
 13 S-1-5-21-518066528-515770016-299552555-2926570 (Group: MYDOMAIN\YetAnotherGroup)
    Attributes - Mandatory Default Enabled
 14 S-1-5-21-661411660-2927047998-133698966-513 (Group: MYDOMAIN\Domain Users)
    Attributes - Mandatory Default Enabled
 15 S-1-5-21-518066528-515770016-299552555-2986081 (Alias: MYDOMAIN\an_alias)
    Attributes - Mandatory Default Enabled GroupResource
 16 S-1-5-21-518066528-515770016-299552555-3037986 (Alias: MYDOMAIN\AReallyLongGroupName1)
    Attributes - Mandatory Default Enabled GroupResource
 17 S-1-5-21-518066528-515770016-299552555-3038991 (Alias: MYDOMAIN\AReallyLongGroupName2)
    Attributes - Mandatory Default Enabled GroupResource
 18 S-1-5-21-518066528-515770016-299552555-3037999 (Alias: MYDOMAIN\AReallyLongGroupName3)
    Attributes - Mandatory Default Enabled GroupResource
 19 S-1-5-21-518066528-515770016-299552555-3038983 (Alias: MYDOMAIN\AReallyReallyLongGroupName)
    Attributes - Mandatory Default Enabled GroupResource
 20 S-1-5-5-0-71188 (no name mapped)
    Attributes - Mandatory Default Enabled LogonId
 21 S-1-2-0 (Well Known Group: localhost\LOCAL)
    Attributes - Mandatory Default Enabled
 22 S-1-5-4 (Well Known Group: NT AUTHORITY\INTERACTIVE)
    Attributes - Mandatory Default Enabled
 23 S-1-5-11 (Well Known Group: NT AUTHORITY\Authenticated Users)
    Attributes - Mandatory Default Enabled
Primary Group: S-1-5-21-518066528-515770016-299552555-513 (Group: MYDOMAIN\Domain Users)
Privs:
 00 0x000000017 SeChangeNotifyPrivilege           Attributes - Enabled Default
 01 0x000000008 SeSecurityPrivilege               Attributes -
 02 0x000000011 SeBackupPrivilege                 Attributes -
 03 0x000000012 SeRestorePrivilege                Attributes -
 04 0x00000000c SeSystemtimePrivilege             Attributes -
 05 0x000000013 SeShutdownPrivilege               Attributes -
 06 0x000000018 SeRemoteShutdownPrivilege         Attributes -
 07 0x000000009 SeTakeOwnershipPrivilege          Attributes -
 08 0x000000014 SeDebugPrivilege                  Attributes -
 09 0x000000016 SeSystemEnvironmentPrivilege      Attributes -
 10 0x00000000b SeSystemProfilePrivilege          Attributes -
 11 0x00000000d SeProfileSingleProcessPrivilege   Attributes -
 12 0x00000000e SeIncreaseBasePriorityPrivilege   Attributes -
 13 0x00000000a SeLoadDriverPrivilege             Attributes - Enabled
 14 0x00000000f SeCreatePagefilePrivilege         Attributes -
 15 0x000000005 SeIncreaseQuotaPrivilege          Attributes -
 16 0x000000019 SeUndockPrivilege                 Attributes - Enabled
 17 0x00000001c SeManageVolumePrivilege           Attributes -
Authentication ID:         (0,11691)
Impersonation Level:       Anonymous
TokenType:                 Primary
Source: User32             TokenFlags: 0x9 ( Token in use )
Token ID: 18296            ParentToken ID: 0
Modified ID:               (0, 18298)
RestrictedSidCount: 0      RestrictedSids: 00000000
```

 

 





