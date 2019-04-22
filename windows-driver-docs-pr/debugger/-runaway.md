---
title: 失控
description: 失控扩展显示有关每个线程使用的时间信息。
ms.assetid: ea318d5b-60c6-4d1c-80c7-6bc418ad01ab
keywords:
- 超越 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- runaway
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: db1da6ce2bf3c95e0ea15f50dcb51ea38a7e9afa
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59238906"
---
# <a name="runaway"></a>!runaway


**！ 失控**扩展显示有关每个线程使用的时间的信息。

```dbgcmd
!runaway [Flags]
```

## <a name="span-idddkrunawaydbgspanspan-idddkrunawaydbgspanparameters"></a><span id="ddk__runaway_dbg"></span><span id="DDK__RUNAWAY_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定要显示的信息类型。 *标志*可以是以下位的任意组合。 默认值为 0x1。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
使调试器以显示每个线程使用的用户数量。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
使调试器以显示每个线程使用的内核时间量。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
使调试器以显示每个线程创建以来已经过去的时间量。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Uext.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p></p>
Uext.dll Ntsdexts.dll</td>
</tr>
</tbody>
</table>

 

**！ 失控**期间实时调试或调试由创建的故障转储文件时，可以仅使用扩展[ **.dump /mt** ](-dump--create-dump-file-.md)或 **.dump /ma**.

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关在用户模式下的线程的信息，请参阅[控制进程和线程](controlling-processes-and-threads.md)。 有关分析进程和线程的详细信息，请参阅*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 

<a name="remarks"></a>备注
-------

此扩展是找出哪些线程都不受控制旋转或占用太多 CPU 时间的快速方法。

显示标识每个线程由调试器的内部线程编号和线程 ID 以十六进制格式。 调试器 Id 也会显示。

下面是一个示例：

```dbgcmd
0:001> !runaway 7

 User Mode Time
 Thread       Time
 0:55c        0:00:00.0093
 1:1a4        0:00:00.0000

 Kernel Mode Time
 Thread       Time
 0:55c        0:00:00.0140
 1:1a4        0:00:00.0000

 Elapsed Time
 Thread       Time
 0:55c        0:00:43.0533
 1:1a4        0:00:25.0876
```

 

 





