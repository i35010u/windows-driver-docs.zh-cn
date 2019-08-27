---
title: processfields
description: Processfields 扩展在执行进程 (EPROCESS) 块中显示字段的名称和偏移量。
ms.assetid: d1d4c49e-3566-4cf6-8b08-656668c92d6c
keywords:
- processfields Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- processfields
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0745a8c1e9abe4fefff1007fb084a6d1b86f3145
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025165"
---
# <a name="processfields"></a>!processfields


**! Processfields** extension 显示执行进程 (EPROCESS) 块内字段的名称和偏移量。

```dbgcmd
!processfields
```

## <span id="ddk__processfields_dbg"></span><span id="DDK__PROCESSFIELDS_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p>不可用 (请参阅 "备注" 部分)</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 EPROCESS 块的信息, 请参阅*Microsoft Windows 内部机制*, 并将 Russinovich 和 David 所罗门群岛标记为。

<a name="remarks"></a>备注
-------

此扩展命令在 Windows XP 或更高版本的 Windows 中不可用。 请改用[**dt (Display Type)** ](dt--display-type-.md)命令直接显示 EPROCESS 结构:

```dbgcmd
kd> dt nt!_EPROCESS 
```

下面是 Windows 2000 系统中 **! processfields**的示例:

```dbgcmd
kd> !processfields
 EPROCESS structure offsets:

    Pcb:                               0x0
    ExitStatus:                        0x6c
    LockEvent:                         0x70
    LockCount:                         0x80
    CreateTime:                        0x88
    ExitTime:                          0x90
    LockOwner:                         0x98
    UniqueProcessId:                   0x9c
    ActiveProcessLinks:                0xa0
    QuotaPeakPoolUsage[0]:             0xa8
    QuotaPoolUsage[0]:                 0xb0
    PagefileUsage:                     0xb8
    CommitCharge:                      0xbc
    PeakPagefileUsage:                 0xc0
    PeakVirtualSize:                   0xc4
    VirtualSize:                       0xc8
    Vm:                                0xd0
    DebugPort:                         0x120
    ExceptionPort:                     0x124
    ObjectTable:                       0x128
    Token:                             0x12c
    WorkingSetLock:                    0x130
    WorkingSetPage:                    0x150
    ProcessOutswapEnabled:             0x154
    ProcessOutswapped:                 0x155
    AddressSpaceInitialized:           0x156
    AddressSpaceDeleted:               0x157
    AddressCreationLock:               0x158
    ForkInProgress:                    0x17c
    VmOperation:                       0x180
    VmOperationEvent:                  0x184
    PageDirectoryPte:                  0x1f0
    LastFaultCount:                    0x18c
    VadRoot:                           0x194
    VadHint:                           0x198
    CloneRoot:                         0x19c
    NumberOfPrivatePages:              0x1a0
    NumberOfLockedPages:               0x1a4
    ForkWasSuccessful:                 0x182
    ExitProcessCalled:                 0x1aa
    CreateProcessReported:             0x1ab
    SectionHandle:                     0x1ac
    Peb:                               0x1b0
    SectionBaseAddress:                0x1b4
    QuotaBlock:                        0x1b8
    LastThreadExitStatus:              0x1bc
    WorkingSetWatch:                   0x1c0
    InheritedFromUniqueProcessId:      0x1c8
    GrantedAccess:                     0x1cc
    DefaultHardErrorProcessing         0x1d0
    LdtInformation:                    0x1d4
    VadFreeHint:                       0x1d8
    VdmObjects:                        0x1dc
    DeviceMap:                         0x1e0
    ImageFileName[0]:                  0x1fc
    VmTrimFaultValue:                  0x20c
    Win32Process:                      0x214
    Win32WindowStation:                0x1c4
```

 

 





