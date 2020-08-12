---
title: 准备好
description: Ready 扩展显示系统中的每个线程处于 "就绪" 状态的摘要信息。
ms.assetid: 1dc94ceb-7d06-4874-999c-059c86f51ea0
keywords:
- 线程，准备好的线程
- 就绪 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ready
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 58822a0bec39ea4c98d96ef349a3c6b9f77e2694
ms.sourcegitcommit: bb3b62a57ba3aea4a0adeefd2d81993367b7b334
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88148431"
---
# <a name="ready"></a>!ready


**！ Ready**扩展显示系统中的每个线程处于就绪状态的摘要信息。

```dbgcmd
!ready [Flags]
```

## <a name="span-idddk__ready_dbgspanspan-idddk__ready_dbgspanparameters"></a><span id="ddk__ready_dbg"></span><span id="DDK__READY_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定要显示的详细信息的级别。 *标志* 可以是以下位的任意组合。 如果 *Flags* 为0，则只显示最少数量的信息。 默认值为0x6。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)   
使显示包含线程的等待状态。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)   
如果包含，但没有位 1 (0x2) ，则不起作用。 如果它与第1位一起提供，则该线程将显示堆栈跟踪。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>第 3 (0x8)   
使每个函数的显示包含返回地址和堆栈指针。 禁止显示函数参数。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位 4 (0x10)   
使每个函数的显示仅包含返回地址;将取消参数和堆栈指针。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关线程计划和就绪状态的信息，请参阅 *Microsoft Windows 内部机制*，标记 Russinovich 和 David 所罗门群岛。 

<a name="remarks"></a>备注
-------

此扩展的输出类似于 [**！线程**](-thread.md)的输出，只不过只显示就绪线程，并按优先级递减顺序进行排序。

 

 





