---
title: SetupAPI 日志记录函数
description: SetupAPI 日志记录函数
ms.assetid: d27bd44c-41c1-4546-b463-11ed3f5c7d84
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15e228720c9372bcb6352a3f03f617b8a1776b40
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386392"
---
# <a name="setupapi-logging-functions"></a>SetupAPI 日志记录函数


从 Windows Vista、 插即用 (PnP) 设备安装应用程序、 类安装程序和共同安装程序可以使用以下函数以将日志项写入[SetupAPI 文本日志](setupapi-text-logs.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken" data-raw-source="[&lt;strong&gt;SetupGetThreadLogToken&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)"><strong>SetupGetThreadLogToken</strong></a></p></td>
<td align="left"><p>检索<a href="log-tokens.md" data-raw-source="[log token](log-tokens.md)">日志令牌</a>的线程的调用<a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken" data-raw-source="[&lt;strong&gt;SetupGetThreadLogToken&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)"> <strong>SetupGetThreadLogToken</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken" data-raw-source="[&lt;strong&gt;SetupSetThreadLogToken&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken)"><strong>SetupSetThreadLogToken</strong></a></p></td>
<td align="left"><p>设置调用的线程的日志标记<a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken" data-raw-source="[&lt;strong&gt;SetupSetThreadLogToken&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken)"> <strong>SetupSetThreadLogToken</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog" data-raw-source="[&lt;strong&gt;SetupWriteTextLog&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)"><strong>SetupWriteTextLog</strong></a></p></td>
<td align="left"><p>写入日志项<a href="setupapi-text-logs.md" data-raw-source="[SetupAPI text log](setupapi-text-logs.md)">SetupAPI 文本日志</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlogerror" data-raw-source="[&lt;strong&gt;SetupWriteTextLogError&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlogerror)"><strong>SetupWriteTextLogError</strong></a></p></td>
<td align="left"><p>有关特定于安装程序 Api 的错误或 Win32 错误 SetupAPI 文本日志中的写入信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextloginfline" data-raw-source="[&lt;strong&gt;SetupWriteTextLogInfLine&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupwritetextloginfline)"><strong>SetupWriteTextLogInfLine</strong></a></p></td>
<td align="left"><p>包含指定的 INF 文件行的文本了 SetupAPI 文本日志中写入日志项。</p></td>
</tr>
</tbody>
</table>

 

 

 





