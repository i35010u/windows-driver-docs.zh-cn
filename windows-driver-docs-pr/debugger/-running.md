---
title: 运行
description: 正在运行的扩展插件都会显示一系列的目标计算机的所有处理器上运行的线程。
ms.assetid: 08fd9806-36e9-4589-bf92-87dc02efebac
keywords:
- 运行 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- running
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: be23896e3bb75514251c78d37c3e5359400aed6b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540960"
---
# <a name="running"></a>！ 运行


**！ 运行**扩展显示的目标计算机的所有处理器上运行的线程的列表。

```dbgcmd
!running [-i] [-t]
```

## <a name="span-idddkrunningdbgspanspan-idddkrunningdbgspanparameters"></a><span id="ddk__running_dbg"></span><span id="DDK__RUNNING_DBG"></span>参数


<span id="_______-i______"></span><span id="_______-I______"></span> **-i**   
将导致显示以包括以及空闲处理器。

<span id="_______-t______"></span><span id="_______-T______"></span> **-t**   
导致要显示的每个处理器的堆栈跟踪。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关调试多处理器计算机的详细信息，请参阅[多处理器语法](multiprocessor-syntax.md)。

<a name="remarks"></a>备注
-------

不带任何选项 **！ 运行**将显示所有活动的处理器和空闲状态的所有处理器的关联。 对于所有活动的处理器，它还会显示当前和下一个线程字段从进程控制块 (PRCB) 和 16 个内置排队的自旋锁的状态。

下面是一个多处理器的 Itanium 系统的示例：

```dbgcmd
0: kd> !running
 
System Processors 3 (affinity mask)
 Idle Processors 0
 
     Prcb              Current           Next
  0  e0000000818f8000  e0000000818f9e50  e0000000866f12f0  ................
 1  e000000086f16010  e00000008620ebe0  e000000086eddbc0  .O..............
```

在每行末尾的 16 字符指示内置的排队的自旋锁 （LockQueue PRCB 中的条目）。 一段 (。 ) 指示锁不是在使用中， **O**意味着锁归此处理器，并**W**意味着处理器将排队，等待该锁定。 若要查看有关数值调节钮锁定队列的详细信息，请使用[ **！ qlocks**](-qlocks.md)。

下面是一个示例，说明活动和空闲的处理器，以及其堆栈跟踪：

```dbgcmd
0: kd> !running -it
 
System Processors f (affinity mask)
  Idle Processors f
All processors idle.
 
     Prcb      Current   Next
  0  ffdff120  805495a0            ................
 
ChildEBP RetAddr
8053e3f0 805329c2 nt!RtlpBreakWithStatusInstruction
8053e3f0 80533464 nt!_KeUpdateSystemTime+0x126
ffdff980 ffdff980 nt!KiIdleLoop+0x14
 
 1  f87e0120  f87e2e60            ................
 
ChildEBP RetAddr
f87e0980 f87e0980 nt!KiIdleLoop+0x14
 
 2  f87f0120  f87f2e60            ................
 
ChildEBP RetAddr
f87f0980 f87f0980 nt!KiIdleLoop+0x14
 
  3  f8800120  f8802e60            ................
 
ChildEBP RetAddr
f8800980 f8800980 nt!KiIdleLoop+0x14
```

 

 





