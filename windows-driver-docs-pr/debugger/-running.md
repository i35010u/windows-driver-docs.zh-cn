---
title: “正在运行”
description: 正在运行的扩展显示目标计算机的所有处理器上正在运行的线程的列表。
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
ms.openlocfilehash: 8f68706554978861f7a5aa737129e9edc5aa08c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805805"
---
# <a name="running"></a>!running


**！运行** 扩展显示目标计算机的所有处理器上正在运行的线程的列表。

```dbgcmd
!running [-i] [-t]
```

## <a name="span-idddk__running_dbgspanspan-idddk__running_dbgspanparameters"></a><span id="ddk__running_dbg"></span><span id="DDK__RUNNING_DBG"></span>参数


<span id="_______-i______"></span><span id="_______-I______"></span>**-i**   
使显示器也包含空闲处理器。

<span id="_______-t______"></span><span id="_______-T______"></span>**-t**   
导致为每个处理器显示堆栈跟踪。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关调试多处理器计算机的详细信息，请参阅 [多处理器语法](multiprocessor-syntax.md)。

<a name="remarks"></a>备注
-------

在没有任何选项的情况下， **运行！运行** 将显示所有活动处理器和所有空闲处理器的关联。 对于所有活动处理器，它还将显示进程控制块中的当前和下一个线程字段 (PRCB) 和16个内置排队自旋锁的状态。

下面是多处理器 Itanium 系统的示例：

```dbgcmd
0: kd> !running
 
System Processors 3 (affinity mask)
 Idle Processors 0
 
     Prcb              Current           Next
  0  e0000000818f8000  e0000000818f9e50  e0000000866f12f0  ................
 1  e000000086f16010  e00000008620ebe0  e000000086eddbc0  .O..............
```

每行末尾的16个字符指示内置的排队自旋锁 (PRCB) 中的 LockQueue 条目。 句点 (。 ) 指示该锁未被使用，则 **O** 表示此处理器拥有此锁，而 **W** 表示处理器排队等待锁定。 若要查看有关旋转锁定队列的详细信息，请使用 [**！ qlocks**](-qlocks.md)。

下面是一个示例，显示了活动和空闲的处理器及其堆栈跟踪：

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

 

 





