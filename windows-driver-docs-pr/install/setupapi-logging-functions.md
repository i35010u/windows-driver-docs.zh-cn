---
title: SetupAPI 日志记录函数
description: SetupAPI 日志记录函数
ms.assetid: d27bd44c-41c1-4546-b463-11ed3f5c7d84
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a118245ea93182b1c938a4a87f22ae9c00b836c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348643"
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552211" data-raw-source="[&lt;strong&gt;SetupGetThreadLogToken&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552211)"><strong>SetupGetThreadLogToken</strong></a></p></td>
<td align="left"><p>检索<a href="log-tokens.md" data-raw-source="[log token](log-tokens.md)">日志令牌</a>的线程的调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff552211" data-raw-source="[&lt;strong&gt;SetupGetThreadLogToken&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552211)"> <strong>SetupGetThreadLogToken</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552216" data-raw-source="[&lt;strong&gt;SetupSetThreadLogToken&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552216)"><strong>SetupSetThreadLogToken</strong></a></p></td>
<td align="left"><p>设置调用的线程的日志标记<a href="https://msdn.microsoft.com/library/windows/hardware/ff552216" data-raw-source="[&lt;strong&gt;SetupSetThreadLogToken&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552216)"> <strong>SetupSetThreadLogToken</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552218" data-raw-source="[&lt;strong&gt;SetupWriteTextLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552218)"><strong>SetupWriteTextLog</strong></a></p></td>
<td align="left"><p>写入日志项<a href="setupapi-text-logs.md" data-raw-source="[SetupAPI text log](setupapi-text-logs.md)">SetupAPI 文本日志</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552232" data-raw-source="[&lt;strong&gt;SetupWriteTextLogError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552232)"><strong>SetupWriteTextLogError</strong></a></p></td>
<td align="left"><p>有关特定于安装程序 Api 的错误或 Win32 错误 SetupAPI 文本日志中的写入信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552236" data-raw-source="[&lt;strong&gt;SetupWriteTextLogInfLine&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552236)"><strong>SetupWriteTextLogInfLine</strong></a></p></td>
<td align="left"><p>包含指定的 INF 文件行的文本了 SetupAPI 文本日志中写入日志项。</p></td>
</tr>
</tbody>
</table>

 

 

 





