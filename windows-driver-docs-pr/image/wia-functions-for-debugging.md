---
title: 用于调试的 WIA 函数
description: 用于调试的 WIA 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8d43270dec862039a116b441243cb69fc84c694
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837737"
---
# <a name="wia-functions-for-debugging"></a>用于调试的 WIA 函数





在开发 WIA 微型驱动程序时，可以使用以下函数记录跟踪消息、警告消息和错误消息。

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
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgdump" data-raw-source="[&lt;strong&gt;wiauDbgDump&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgdump)"><strong>wiauDbgDump</strong></a></p></td>
<td><p>记录包含一个或多个数据值的消息。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgerror" data-raw-source="[&lt;strong&gt;wiauDbgError&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgerror)"><strong>wiauDbgError</strong></a></p></td>
<td><p>记录错误消息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgerrorhr" data-raw-source="[&lt;strong&gt;wiauDbgErrorHr&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgerrorhr)"><strong>wiauDbgErrorHr</strong></a></p></td>
<td><p>记录包含 HRESULT 及其错误消息字符串的消息。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgflags" data-raw-source="[&lt;strong&gt;wiauDbgFlags&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgflags)"><strong>wiauDbgFlags</strong></a></p></td>
<td><p>确定是否设置了特定的调试标志。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbghelper" data-raw-source="[&lt;strong&gt;wiauDbgHelper&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbghelper)"><strong>wiauDbgHelper</strong></a></p></td>
<td><p>设置消息的格式，并将其写入日志文件或调试器。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbghelper2" data-raw-source="[&lt;strong&gt;wiauDbgHelper2&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbghelper2)"><strong>wiauDbgHelper2</strong></a></p></td>
<td><p>将消息写入日志文件或调试器，或同时写入这两者。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbginit" data-raw-source="[&lt;strong&gt;wiauDbgInit&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbginit)"><strong>wiauDbgInit</strong></a></p></td>
<td><p>初始化 WIA 调试。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacyerror" data-raw-source="[&lt;strong&gt;wiauDbgLegacyError&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacyerror)"><strong>wiauDbgLegacyError</strong></a></p></td>
<td><p>记录错误消息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacyerror2" data-raw-source="[&lt;strong&gt;wiauDbgLegacyError2&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacyerror2)"><strong>wiauDbgLegacyError2</strong></a></p></td>
<td><p>记录错误消息。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacyhresult2" data-raw-source="[&lt;strong&gt;wiauDbgLegacyHresult2&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacyhresult2)"><strong>wiauDbgLegacyHresult2</strong></a></p></td>
<td><p>记录包含 HRESULT 的默认消息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacytrace" data-raw-source="[&lt;strong&gt;wiauDbgLegacyTrace&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacytrace)"><strong>wiauDbgLegacyTrace</strong></a></p></td>
<td><p>记录跟踪消息。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacytrace2" data-raw-source="[&lt;strong&gt;wiauDbgLegacyTrace2&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacytrace2)"><strong>wiauDbgLegacyTrace2</strong></a></p></td>
<td><p>记录跟踪消息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacywarning" data-raw-source="[&lt;strong&gt;wiauDbgLegacyWarning&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacywarning)"><strong>wiauDbgLegacyWarning</strong></a></p></td>
<td><p>记录一条警告消息。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgsetflags" data-raw-source="[&lt;strong&gt;wiauDbgSetFlags&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgsetflags)"><strong>wiauDbgSetFlags</strong></a></p></td>
<td><p>设置调试标志。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgtrace" data-raw-source="[&lt;strong&gt;wiauDbgTrace&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgtrace)"><strong>wiauDbgTrace</strong></a></p></td>
<td><p>记录跟踪消息。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgwarning" data-raw-source="[&lt;strong&gt;wiauDbgWarning&lt;/strong&gt;](/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgwarning)"><strong>wiauDbgWarning</strong></a></p></td>
<td><p>记录一条警告消息。</p></td>
</tr>
</tbody>
</table>

 

