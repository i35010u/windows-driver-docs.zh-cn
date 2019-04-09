---
title: sprocess
description: Sprocess 扩展指定会话中显示有关指定的会话过程中，或所有进程的信息。
ms.assetid: 03c69f3c-501a-44e4-98e0-bf851ca6d24e
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
ms.openlocfilehash: f7e00edfb5e961ad936a0b14a51ce963acb4b25f
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239642"
---
# <a name="sprocess"></a>!sprocess


**！ Sprocess**扩展指定会话中显示有关指定的会话过程中，或所有进程的信息。

```dbgcmd
!sprocess Session [Flags [ImageName]] 
!sprocess -?
```

## <a name="span-idddksprocessdbgspanspan-idddksprocessdbgspanparameters"></a><span id="ddk__sprocess_dbg"></span><span id="DDK__SPROCESS_DBG"></span>参数


<span id="_______Session______"></span><span id="_______session______"></span><span id="_______SESSION______"></span> *会话*   
指定拥有所需的进程的会话。 *会话*始终解释为十进制数。

*会话*可以具有以下值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>-1</p></td>
<td align="left"><p>使用当前会话。 这是默认设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>-2</p></td>
<td align="left"><p>使用<a href="changing-contexts.md#session-context" data-raw-source="[session context](changing-contexts.md#session-context)">会话上下文</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>-4</p></td>
<td align="left"><p>显示由会话的所有进程。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
在显示中指定详细信息的级别。 *标志*可以是以下位的任意组合。 默认值为 0。

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
<td align="left"><p>位 0 (0x1)</p></td>
<td align="left"><p>显示时间和优先级的统计信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>位 1 (0x2)</p></td>
<td align="left"><p>将添加到显示线程和进程和线程的等待状态与关联的事件的列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p>位 2 (0x4)</p></td>
<td align="left"><p>将添加到显示与该进程关联的线程的列表。 如果不包含位 1 (0x2) 使用此位，则在单个行上显示每个线程。 如果这是附带位 1，与堆栈跟踪显示每个线程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>位 3 (0x8)</p></td>
<td align="left"><p>将添加到显示的每个函数的返回地址的堆栈指针并在基于 Itanium 的系统<strong>bsp</strong>注册值。 它取消函数自变量的显示。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4 位 (0x10)</p></td>
<td align="left"><p>显示仅返回每个函数的地址。 禁止显示参数和堆栈指针。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______ImageName______"></span><span id="_______imagename______"></span><span id="_______IMAGENAME______"></span> *ImageName*   
指定要显示的进程的名称。 其可执行映像名匹配的所有进程*ImageName*显示。 映像名称必须与匹配 EPROCESS 块中。 一般情况下，这是调用启动进程，包括文件扩展名 (通常为.exe)，并截断后的第 15 个字符时可执行文件名称。 没有方法来指定包含空格的映像名称。

<span id="_______-_______"></span> **-?**   
显示此扩展在调试器命令窗口中的帮助。 此帮助文本具有一些遗漏。

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

有关会话和进程在内核模式下的信息，请参阅[更改上下文](changing-contexts.md)。 有关分析进程和线程的详细信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 

<a name="remarks"></a>备注
-------

此扩展的输出是类似于[ **！ 过程**](-process.md)，只不过的地址\_MM\_会话\_空间和\_MMSESSION 是还显示。

 

 





