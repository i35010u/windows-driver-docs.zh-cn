---
title: threadfields
description: Threadfields 扩展显示名称和 executive 线程 (ETHREAD) 块中的字段的偏移量。
ms.assetid: 1b36e922-9079-4dc5-911a-f635ec026084
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
ms.openlocfilehash: 83e496d76ee22a7b2cdb1743aaaf3f7a1079701f
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239180"
---
# <a name="threadfields"></a>!threadfields


**！ Threadfields**扩展显示名称和 executive 线程 (ETHREAD) 块中的字段的偏移量。

```dbgcmd
!threadfields
```

## <span id="ddk__threadfields_dbg"></span><span id="DDK__THREADFIELDS_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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
<td align="left"><p>不可用 （请参阅备注部分）</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

ETHREAD 块有关的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 

<a name="remarks"></a>备注
-------

此扩展命令不可在 Windows XP 或更高版本的 Windows 中可用。 请改用[ **dt （显示类型）** ](dt--display-type-.md)命令直接显示 ETHREAD 结构：

```dbgcmd
kd> dt nt!_ETHREAD 
```

下面是举例 **！ threadfields**从 Windows 2000 系统：

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

 

 





