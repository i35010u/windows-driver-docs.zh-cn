---
title: 缓冲区 DbgPrint 输出
description: 缓冲区 DbgPrint 输出
keywords:
- '全局标志 (的缓冲区 DbgPrint 输出) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f51ddade9dc07bdecb356953765bd395daca359
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788865"
---
# <a name="buffer-dbgprint-output"></a>缓冲区 DbgPrint 输出


## <span id="ddk_buffer_dbgprint_output_dtools"></span><span id="DDK_BUFFER_DBGPRINT_OUTPUT_DTOOLS"></span>


**Buffer DbgPrint output** 标志禁止调试程序从 **DbgPrint**、 **DbgPrintEx**、 **KdPrint** 和 **KdPrintEx** 调用输出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>ddp</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x08000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_DISABLE_DBGPRINT</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围内的注册表项，内核标志</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

当取消调试器输出时，它不会自动出现在内核调试器中。 但是，消息始终发送到 DbgPrint 缓冲区，可在其中使用 [**！ DbgPrint**](-dbgprint.md) 调试程序扩展访问该消息。

有关与调试器通信的函数的信息，请参阅将 [输出发送到调试器](sending-output-to-the-debugger.md)。

 

 





