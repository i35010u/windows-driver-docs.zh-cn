---
title: threadfields
description: Threadfields 扩展在 ETHREAD) 块 (的执行线程中显示字段的名称和偏移量。
keywords:
- threadfields Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- threadfields
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3ac9f3bf9440f781d01d60dddd6860def12ab957
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830301"
---
# <a name="threadfields"></a>!threadfields


**！ Threadfields** 扩展显示 (ETHREAD) 块的执行线程中的字段的名称和偏移量。

```dbgcmd
!threadfields
```

## <span id="ddk__threadfields_dbg"></span><span id="DDK__THREADFIELDS_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p> (，请参阅 "备注" 部分) </p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 ETHREAD 块的信息，请参阅 *Microsoft Windows 内部机制*，并将 Russinovich 和 David 所罗门群岛标记为。 

<a name="remarks"></a>备注
-------

此扩展命令在 Windows XP 或更高版本的 Windows 中不可用。 请改用 [**dt (显示类型)**](dt--display-type-.md) 命令，直接显示 ETHREAD 结构：

```dbgcmd
kd> dt nt!_ETHREAD 
```

下面是 Windows 2000 系统中 **！ threadfields** 的示例：

```dbgcmd
kd> !threadfields
 ETHREAD structure offsets:

    Tcb:                           0x0
    CreateTime:                    0x1b0
    ExitTime:                      0x1b8
    ExitStatus:                    0x1c0
    PostBlockList:                 0x1c4
    TerminationPortList:           0x1cc
    ActiveTimerListLock:           0x1d4
    ActiveTimerListHead:           0x1d8
    Cid:                           0x1e0
    LpcReplySemaphore:             0x1e8
    LpcReplyMessage:               0x1fc
    LpcReplyMessageId:             0x200
    ImpersonationInfo:             0x208
    IrpList:                       0x20c
    TopLevelIrp:                   0x214
    ReadClusterSize:               0x21c
    ForwardClusterOnly:            0x220
    DisablePageFaultClustering:    0x221
    DeadThread:                    0x222
    HasTerminated:                 0x224
    GrantedAccess:                 0x228
    ThreadsProcess:                0x22c
    StartAddress:                  0x230
    Win32StartAddress:             0x234
    LpcExitThreadCalled:           0x238
    HardErrorsAreDisabled:         0x239
```

 

 





