---
title: 准备就绪
description: 准备扩展处于就绪状态系统中显示有关每个线程的摘要信息。
ms.assetid: 1dc94ceb-7d06-4874-999c-059c86f51ea0
keywords:
- 线程就绪线程
- 准备 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ready
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 096c3cf2b89b08b56345c245f888bb35e8a3b507
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239526"
---
# <a name="ready"></a>!ready


**！ 准备**扩展处于就绪状态系统中显示有关每个线程的摘要信息。

```dbgcmd
!ready [Flags]
```

## <a name="span-idddkreadydbgspanspan-idddkreadydbgspanparameters"></a><span id="ddk__ready_dbg"></span><span id="DDK__READY_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定要显示详细信息的级别。 *标志*可以是以下位的任意组合。 如果*标志*为 0，则显示只有少量的信息。 默认值为 0x6。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
将导致显示以包括线程的等待状态。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
如果这是包含不带位 1 (0x2)，这没有任何影响。 如果这是随附位 1，线程被显示堆栈跟踪。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
显示每个函数返回地址，堆栈指针，并 （在 Itanium 系统） 将导致**bsp**注册值。 取消函数自变量的显示。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>4 位 (0x10)  
将导致显示的每个函数，以包含仅返回的地址;取消自变量和堆栈指针。

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
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关线程计划和就绪状态的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 

<a name="remarks"></a>备注
-------

此扩展的输出是类似于[ **！ 线程**](-thread.md)，只不过显示仅就绪线程，并且它们降低优先级的顺序进行排序。

 

 





