---
title: 缓冲区 DbgPrint 输出
description: 缓冲区 DbgPrint 输出
ms.assetid: af97c484-3a37-4c86-8828-12a0ea1c8c0e
keywords:
- 缓冲区 DbgPrint 输出 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: db5634202fcb99544309cf2304aebdc3ddad9aa9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347847"
---
# <a name="buffer-dbgprint-output"></a>缓冲区 DbgPrint 输出


## <span id="ddk_buffer_dbgprint_output_dtools"></span><span id="DDK_BUFFER_DBGPRINT_OUTPUT_DTOOLS"></span>


**缓冲区 DbgPrint 输出**标志将取消调试器输出**DbgPrint**， **DbgPrintEx**， **KdPrint**，和**KdPrintEx**调用。

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
<td align="left"><p>整个系统的注册表项，内核标志</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

当调试器输出被禁止显示，它不会自动出现在内核调试程序。 但是，该消息总是发送到 DbgPrint 缓冲区，然后它可以通过访问[ **！ dbgprint** ](-dbgprint.md)调试器扩展。

与调试器有关的函数进行通信的信息，请参阅[将输出发送到调试器](sending-output-to-the-debugger.md)。

 

 





