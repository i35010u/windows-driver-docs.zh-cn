---
title: iovirp
description: Iovirp 扩展显示指定 i/o 验证程序 IRP 的详细信息。
keywords:
- I/o 验证程序
- iovirp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- iovirp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 26582133e454113a0bcb8ee68b61d68b8773326f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788939"
---
# <a name="iovirp"></a>!iovirp


**！ Iovirp** extension 显示指定 i/o 验证程序 IRP 的详细信息。

```dbgcmd
!iovirp [IRP]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______IRP______"></span><span id="_______irp______"></span>*IRP*   
指定由驱动程序验证程序跟踪的 IRP 的地址。 如果 *IRP* 为0或被省略，则显示每个未完成 IRP 的摘要信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

下面是此扩展的输出示例：

```dbgcmd
kd> !iovirp 947cef68
IovPacket       84509af0
TrackedIrp      947cef68
HeaderLock      84509d61
LockIrql        0
ReferenceCount  1
PointerCount    1
HeaderFlags     00000000
ChainHead       84509af0
Flags           00200009
DepartureIrql   0
ArrivalIrql     0
StackCount      1
QuotaCharge     00000000
QuotaProcess    0
RealIrpCompletionRoutine        0
RealIrpControl                  0
RealIrpContext                  0
TopStackLocation        2
PriorityBoost           0
LastLocation            0
RefTrackingCount        0
SystemDestVA            0
VerifierSettings        84509d08
pIovSessionData         84509380
Allocation Stack:
  nt!IovAllocateIrp+1a  (817df356)
 nt!IopXxxControlFile+40c  (8162de20)
  nt!NtDeviceIoControlFile+2a  (81633090)
 nt!KiFastCallEntry+164  (81513c64)
  nt!EtwpFlushBuffer+10f  (817606d7)
  nt!EtwpFlushBuffersWithMarker+bd  (817608cb)
  nt!EtwpFlushActiveBuffers+2b4  (81760bc2)
  nt!EtwpLogger+213  (8176036f)
```

您可以通过在 WinDbg) 中按 CTRL + BREAK (或在 KD) 中按 CTRL + C (，随时停止执行。

 

 





