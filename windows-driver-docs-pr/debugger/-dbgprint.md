---
title: dbgprint
description: Dbgprint 扩展显示以前发送到 DbgPrint 缓冲区的字符串。
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
ms.openlocfilehash: b56c28abff38a2de993635a20bb08d3d3ed27958
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792053"
---
# <a name="dbgprint"></a>!dbgprint


**！ Dbgprint** extension 显示以前发送到 **dbgprint** 缓冲区的字符串。

```dbgcmd
!dbgprint
```

## <span id="ddk__dbgprint_dbg"></span><span id="DDK__DBGPRINT_DBG"></span>


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
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 **DbgPrint**、 **KdPrint**、 **DbgPrintEx** 和 **KdPrintEx** 的信息，请参阅将 [输出发送到调试器](sending-output-to-the-debugger.md)。

<a name="remarks"></a>备注
-------

内核模式例程 **DbgPrint**、 **KdPrint**、 **DbgPrintEx** 和 **KdPrintEx** 向目标计算机上的缓冲区发送格式化的字符串。 除非禁用了此类打印，否则该字符串会自动显示在主计算机上的调试器命令窗口中。

通常，发送到此缓冲区的消息将自动显示在调试器命令窗口中。 但是，可以通过全局标志 ( # A0) 实用工具禁用此显示。 此外，在本地内核调试过程中不会自动显示此显示。 有关详细信息，请参阅 [读取和筛选调试消息](reading-and-filtering-debugging-messages.md)中的 "DbgPrint Buffer"。

**！ Dbgprint** 扩展会导致 (显示此缓冲区的内容，而不管是否) 禁用了自动打印。 它不会显示基于其组件和重要性级别筛选掉的消息。  (有关此筛选的详细信息，请参阅 [读取和筛选调试消息](reading-and-filtering-debugging-messages.md)。 ) 

 

 





