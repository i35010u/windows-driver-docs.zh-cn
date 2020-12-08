---
title: 失控
description: 失控扩展显示每个线程占用的时间的相关信息。
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
ms.openlocfilehash: d4098b601f122f728cb7b1e927e1cac5b94f273c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813329"
---
# <a name="runaway"></a>!runaway


**！失控** 扩展显示每个线程占用的时间的相关信息。

```dbgcmd
!runaway [Flags]
```

## <a name="span-idddk__runaway_dbgspanspan-idddk__runaway_dbgspanparameters"></a><span id="ddk__runaway_dbg"></span><span id="DDK__RUNAWAY_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定要显示的信息的类型。 *标志* 可以是以下位的任意组合。 默认值为0x1。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)   
使调试器显示每个线程所使用的用户时间量。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
使调试器显示每个线程占用的内核时间量。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
使调试器显示自创建每个线程以来经过的时间量。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

**！失控** 扩展只能在实时调试过程中使用 **，也不** 能在调试 [**创建的故障**](-dump--create-dump-file-.md)转储文件时使用。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关用户模式下的线程的信息，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。 有关分析进程和线程的详细信息，请参阅 Russinovich 和 David 所罗门群岛的 *Microsoft Windows 内部机制* 。 

<a name="remarks"></a>备注
-------

此扩展可以快速找出哪些线程正在控制或消耗过多的 CPU 时间。

显示由调试器的内部线程编号和十六进制中的线程 ID 标识每个线程。 还显示了调试器 Id。

以下是示例：

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

 

 





