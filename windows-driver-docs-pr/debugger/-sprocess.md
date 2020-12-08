---
title: sprocess
description: Sprocess 扩展显示有关指定会话过程的信息，或有关指定会话中所有进程的信息。
keywords:
- sprocess Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sprocess
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ab073542fcc1bddebd1418a80302813457f2d9d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811249"
---
# <a name="sprocess"></a>!sprocess


**！ Sprocess** 扩展显示有关指定会话过程的信息，或有关指定会话中所有进程的信息。

```dbgcmd
!sprocess Session [Flags [ImageName]] 
!sprocess -?
```

## <a name="span-idddk__sprocess_dbgspanspan-idddk__sprocess_dbgspanparameters"></a><span id="ddk__sprocess_dbg"></span><span id="DDK__SPROCESS_DBG"></span>参数


<span id="_______Session______"></span><span id="_______session______"></span><span id="_______SESSION______"></span>*会话*   
指定拥有所需进程的会话。 *会话* 始终解释为十进制数字。

*会话* 可以具有以下值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>-1</p></td>
<td align="left"><p>使用当前会话。 这是默认值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>-2</p></td>
<td align="left"><p>使用 <a href="changing-contexts.md#session-context" data-raw-source="[session context](changing-contexts.md#session-context)">会话上下文</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>-4</p></td>
<td align="left"><p>按会话显示所有进程。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定显示中的详细信息级别。 *标志* 可以是以下位的任意组合。 默认值为 0。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>显示最少信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>位 0 (0x1) </p></td>
<td align="left"><p>显示时间和优先级统计信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>位 1 (0x2) </p></td>
<td align="left"><p>向显示与进程和线程的等待状态关联的线程和事件的列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p>位 2 (0x4) </p></td>
<td align="left"><p>向显示与进程关联的线程的列表。 如果在没有位 1 (0x2) 的情况下使用此位，则每个线程都显示在单个行中。 如果它包含在第1位，则每个线程都将显示堆栈跟踪。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>第 3 (0x8) </p></td>
<td align="left"><p>向每个函数的显示添加返回地址、堆栈指针和基于 Itanium 的系统上的 " <strong>bsp</strong> 寄存器" 值。 它禁止显示函数自变量。</p></td>
</tr>
<tr class="even">
<td align="left"><p>位 4 (0x10) </p></td>
<td align="left"><p>仅显示每个函数的返回地址。 禁止参数和堆栈指针。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______ImageName______"></span><span id="_______imagename______"></span><span id="_______IMAGENAME______"></span>*ImageName*   
指定要显示的进程的名称。 显示其可执行图像名称与 *ImageName* 匹配的所有进程。 映像名称必须与 EPROCESS 块中的名称匹配。 通常，这是用于启动进程的可执行文件名称，包括文件扩展名 (通常 .exe) ，并在第15个字符之后截断。 没有办法指定包含空格的图像名称。

<span id="_______-_______"></span> **-?**   
在调试器中显示此扩展的帮助命令窗口。 此帮助文本有一些遗漏的内容。

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

有关内核模式下的会话和进程的信息，请参阅 [更改上下文](changing-contexts.md)。 有关分析进程和线程的详细信息，请参阅 Russinovich 和 David 所罗门群岛的 *Microsoft Windows 内部机制*。 

<a name="remarks"></a>备注
-------

此扩展的输出类似于 [**！进程**](-process.md)的输出，只不过 \_ \_ \_ \_ 还会显示 MM 会话空间和 MMSESSION 的地址。

 

 





