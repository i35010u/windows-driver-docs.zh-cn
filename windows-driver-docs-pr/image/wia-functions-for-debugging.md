---
title: 用于调试的 WIA 函数
description: 用于调试的 WIA 函数
ms.assetid: 164eeab3-1e4a-46de-99db-28b8f63593a4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44f2e062984069fb896adc43a39a2e9d5b3c53ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377685"
---
# <a name="wia-functions-for-debugging"></a>用于调试的 WIA 函数





开发您 WIA 微型驱动程序时，可以使用日志跟踪消息、 警告消息和错误消息的以下函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbgdump" data-raw-source="[&lt;strong&gt;wiauDbgDump&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbgdump)"><strong>wiauDbgDump</strong></a></p></td>
<td><p>记录消息包含一个或多个数据值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbgerror" data-raw-source="[&lt;strong&gt;wiauDbgError&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbgerror)"><strong>wiauDbgError</strong></a></p></td>
<td><p>记录一条错误消息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbgerrorhr" data-raw-source="[&lt;strong&gt;wiauDbgErrorHr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbgerrorhr)"><strong>wiauDbgErrorHr</strong></a></p></td>
<td><p>记录消息包含 HRESULT 和错误消息字符串。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbgflags" data-raw-source="[&lt;strong&gt;wiauDbgFlags&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbgflags)"><strong>wiauDbgFlags</strong></a></p></td>
<td><p>确定是否设置了特定的调试标志。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbghelper" data-raw-source="[&lt;strong&gt;wiauDbgHelper&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbghelper)"><strong>wiauDbgHelper</strong></a></p></td>
<td><p>设置消息的格式并将其写入到日志文件或调试器。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbghelper2" data-raw-source="[&lt;strong&gt;wiauDbgHelper2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbghelper2)"><strong>wiauDbgHelper2</strong></a></p></td>
<td><p>向日志文件，调试器，和 / 或写入消息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbginit" data-raw-source="[&lt;strong&gt;wiauDbgInit&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbginit)"><strong>wiauDbgInit</strong></a></p></td>
<td><p>初始化 WIA 调试。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbglegacyerror" data-raw-source="[&lt;strong&gt;wiauDbgLegacyError&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbglegacyerror)"><strong>wiauDbgLegacyError</strong></a></p></td>
<td><p>记录一条错误消息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbglegacyerror2" data-raw-source="[&lt;strong&gt;wiauDbgLegacyError2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbglegacyerror2)"><strong>wiauDbgLegacyError2</strong></a></p></td>
<td><p>记录一条错误消息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbglegacyhresult2" data-raw-source="[&lt;strong&gt;wiauDbgLegacyHresult2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbglegacyhresult2)"><strong>wiauDbgLegacyHresult2</strong></a></p></td>
<td><p>记录包含 HRESULT 的默认消息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbglegacytrace" data-raw-source="[&lt;strong&gt;wiauDbgLegacyTrace&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbglegacytrace)"><strong>wiauDbgLegacyTrace</strong></a></p></td>
<td><p>记录跟踪消息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbglegacytrace2" data-raw-source="[&lt;strong&gt;wiauDbgLegacyTrace2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbglegacytrace2)"><strong>wiauDbgLegacyTrace2</strong></a></p></td>
<td><p>记录跟踪消息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbglegacywarning" data-raw-source="[&lt;strong&gt;wiauDbgLegacyWarning&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbglegacywarning)"><strong>wiauDbgLegacyWarning</strong></a></p></td>
<td><p>记录一条警告消息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbgsetflags" data-raw-source="[&lt;strong&gt;wiauDbgSetFlags&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbgsetflags)"><strong>wiauDbgSetFlags</strong></a></p></td>
<td><p>调试标志的设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbgtrace" data-raw-source="[&lt;strong&gt;wiauDbgTrace&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbgtrace)"><strong>wiauDbgTrace</strong></a></p></td>
<td><p>记录跟踪消息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbgwarning" data-raw-source="[&lt;strong&gt;wiauDbgWarning&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaudbgwarning)"><strong>wiauDbgWarning</strong></a></p></td>
<td><p>记录一条警告消息。</p></td>
</tr>
</tbody>
</table>

 

 

 




