---
title: iovirp
description: Iovirp 扩展显示有关指定的 I/O 验证工具 IRP 的详细的信息。
ms.assetid: 9b05061c-2a57-4e01-bbe0-2e2f5f676947
keywords:
- I/O 验证程序
- iovirp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- iovirp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 27248b4fa1cee453f8bf9c7d33092688d5aec5ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544256"
---
# <a name="iovirp"></a>!iovirp


**！ Iovirp**扩展显示指定的 I/O 验证工具 IRP 的详细的信息。

```dbgcmd
!iovirp [IRP]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______IRP______"></span><span id="_______irp______"></span> *IRP*   
指定跟踪的 Driver Verifier IRP 的地址。 如果*IRP*为 0 或省略，将显示每个未完成的 IRP 的摘要信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

下面是输出的来自此扩展插件示例：

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

可以通过按 CTRL + BREAK （在 WinDbg) 或 CTRL + C （中 KD) 来停止执行任何时候。

 

 





