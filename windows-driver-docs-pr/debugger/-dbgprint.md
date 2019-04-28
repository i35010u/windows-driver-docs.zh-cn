---
title: dbgprint
description: Dbgprint 扩展显示以前已发送到 DbgPrint 缓冲区的字符串。
ms.assetid: bf25ac2a-5a07-43df-946b-3b2237b1816b
keywords:
- dbgprint Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dbgprint
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 00281b2d5f6a389d1dd15c02d9015e4fddabfc79
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336861"
---
# <a name="dbgprint"></a>!dbgprint


**！ Dbgprint**扩展插件都会显示以前已发送到一个字符串**DbgPrint**缓冲区。

```dbgcmd
!dbgprint
```

## <span id="ddk__dbgprint_dbg"></span><span id="DDK__DBGPRINT_DBG"></span>


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

璝惠**DbgPrint**， **KdPrint**， **DbgPrintEx**，并**KdPrintEx**，请参阅[将输出发送到调试器](sending-output-to-the-debugger.md)。

<a name="remarks"></a>备注
-------

内核模式例程**DbgPrint**， **KdPrint**， **DbgPrintEx**，以及**KdPrintEx**将格式化的字符串发送到目标系统上的缓冲区计算机。 字符串会自动显示在主计算机上的调试器命令窗口，除非禁用此类打印。

通常情况下，在调试器命令窗口中自动显示发送到此缓冲区的消息。 但是，可以通过全局标志 (gflags.exe) 实用程序禁用此显示。 此外，此显示不会不自动显示在本地内核调试过程中。 有关详细信息，请参阅[DbgPrint 缓冲区](reading-and-filtering-debugging-messages.md#the-dbgprint-buffer)。

**！ Dbgprint**扩展会导致此缓冲区 （而不考虑是否自动打印已被禁用） 显示的内容。 它不会显示已筛选出基于其组件和重要性级别的消息。 (有关此筛选的详细信息，请参阅[读取和筛选调试消息](reading-and-filtering-debugging-messages.md)。)

 

 





