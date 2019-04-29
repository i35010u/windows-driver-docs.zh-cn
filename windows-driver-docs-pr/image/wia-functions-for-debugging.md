---
title: 用于调试的 WIA 函数
description: 用于调试的 WIA 函数
ms.assetid: 164eeab3-1e4a-46de-99db-28b8f63593a4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25de71792686b2927acc5253190bd144db5109d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380935"
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549627" data-raw-source="[&lt;strong&gt;wiauDbgDump&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549627)"><strong>wiauDbgDump</strong></a></p></td>
<td><p>记录消息包含一个或多个数据值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549633" data-raw-source="[&lt;strong&gt;wiauDbgError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549633)"><strong>wiauDbgError</strong></a></p></td>
<td><p>记录一条错误消息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549637" data-raw-source="[&lt;strong&gt;wiauDbgErrorHr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549637)"><strong>wiauDbgErrorHr</strong></a></p></td>
<td><p>记录消息包含 HRESULT 和错误消息字符串。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549643" data-raw-source="[&lt;strong&gt;wiauDbgFlags&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549643)"><strong>wiauDbgFlags</strong></a></p></td>
<td><p>确定是否设置了特定的调试标志。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549649" data-raw-source="[&lt;strong&gt;wiauDbgHelper&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549649)"><strong>wiauDbgHelper</strong></a></p></td>
<td><p>设置消息的格式并将其写入到日志文件或调试器。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549653" data-raw-source="[&lt;strong&gt;wiauDbgHelper2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549653)"><strong>wiauDbgHelper2</strong></a></p></td>
<td><p>向日志文件，调试器，和 / 或写入消息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549660" data-raw-source="[&lt;strong&gt;wiauDbgInit&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549660)"><strong>wiauDbgInit</strong></a></p></td>
<td><p>初始化 WIA 调试。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549667" data-raw-source="[&lt;strong&gt;wiauDbgLegacyError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549667)"><strong>wiauDbgLegacyError</strong></a></p></td>
<td><p>记录一条错误消息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549671" data-raw-source="[&lt;strong&gt;wiauDbgLegacyError2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549671)"><strong>wiauDbgLegacyError2</strong></a></p></td>
<td><p>记录一条错误消息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549675" data-raw-source="[&lt;strong&gt;wiauDbgLegacyHresult2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549675)"><strong>wiauDbgLegacyHresult2</strong></a></p></td>
<td><p>记录包含 HRESULT 的默认消息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550150" data-raw-source="[&lt;strong&gt;wiauDbgLegacyTrace&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550150)"><strong>wiauDbgLegacyTrace</strong></a></p></td>
<td><p>记录跟踪消息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550152" data-raw-source="[&lt;strong&gt;wiauDbgLegacyTrace2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550152)"><strong>wiauDbgLegacyTrace2</strong></a></p></td>
<td><p>记录跟踪消息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550156" data-raw-source="[&lt;strong&gt;wiauDbgLegacyWarning&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550156)"><strong>wiauDbgLegacyWarning</strong></a></p></td>
<td><p>记录一条警告消息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550159" data-raw-source="[&lt;strong&gt;wiauDbgSetFlags&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550159)"><strong>wiauDbgSetFlags</strong></a></p></td>
<td><p>调试标志的设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550161" data-raw-source="[&lt;strong&gt;wiauDbgTrace&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550161)"><strong>wiauDbgTrace</strong></a></p></td>
<td><p>记录跟踪消息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550163" data-raw-source="[&lt;strong&gt;wiauDbgWarning&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550163)"><strong>wiauDbgWarning</strong></a></p></td>
<td><p>记录一条警告消息。</p></td>
</tr>
</tbody>
</table>

 

 

 




