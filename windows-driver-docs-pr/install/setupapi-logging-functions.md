---
title: SetupAPI 日志记录函数
description: SetupAPI 日志记录函数
ms.assetid: d27bd44c-41c1-4546-b463-11ed3f5c7d84
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89746b8bbe38364a44917c0463f1856dbc13b535
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107010"
---
# <a name="setupapi-logging-functions"></a>SetupAPI 日志记录函数


从 Windows Vista 开始，即插即用 (PnP) 设备安装应用程序、类安装程序和共同安装程序可以使用以下函数将日志条目写入 [setupapi.log 文本日志](setupapi-text-logs.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken" data-raw-source="[&lt;strong&gt;SetupGetThreadLogToken&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)"><strong>SetupGetThreadLogToken</strong></a></p></td>
<td align="left"><p>检索名为<a href="/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken" data-raw-source="[&lt;strong&gt;SetupGetThreadLogToken&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupgetthreadlogtoken)"><strong>SetupGetThreadLogToken</strong></a>的线程的<a href="log-tokens.md" data-raw-source="[log token](log-tokens.md)">日志标记</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken" data-raw-source="[&lt;strong&gt;SetupSetThreadLogToken&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken)"><strong>SetupSetThreadLogToken</strong></a></p></td>
<td align="left"><p>设置名为 <a href="/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken" data-raw-source="[&lt;strong&gt;SetupSetThreadLogToken&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupsetthreadlogtoken)"><strong>SetupSetThreadLogToken</strong></a>的线程的日志令牌。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog" data-raw-source="[&lt;strong&gt;SetupWriteTextLog&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlog)"><strong>SetupWriteTextLog</strong></a></p></td>
<td align="left"><p>在 <a href="setupapi-text-logs.md" data-raw-source="[SetupAPI text log](setupapi-text-logs.md)">setupapi.log 文本日志</a>中写入日志项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlogerror" data-raw-source="[&lt;strong&gt;SetupWriteTextLogError&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupwritetextlogerror)"><strong>SetupWriteTextLogError</strong></a></p></td>
<td align="left"><p>在 Setupapi.log 文本日志中写入有关 Setupapi.log 特定错误或 Win32 错误的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/setupapi/nf-setupapi-setupwritetextloginfline" data-raw-source="[&lt;strong&gt;SetupWriteTextLogInfLine&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupwritetextloginfline)"><strong>SetupWriteTextLogInfLine</strong></a></p></td>
<td align="left"><p>在 Setupapi.log 文本日志中写入一个日志项，该日志项包含指定的 INF 文件行的文本。</p></td>
</tr>
</tbody>
</table>

 

