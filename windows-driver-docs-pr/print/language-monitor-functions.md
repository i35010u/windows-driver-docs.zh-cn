---
title: 语言监视器函数
description: 语言监视器函数
keywords:
- 语言监视 WDK 打印、功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b0d73a83665b309cc5d15c506116e1a91a36232
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796481"
---
# <a name="language-monitor-functions"></a>语言监视器函数





下表列出了语言监视器必须定义的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数名称</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DllEntryPoint</strong></p></td>
<td><p>DLL 入口点，通常称为 <strong>DllMain</strong>，如 Microsoft Windows SDK 文档中所述。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeport" data-raw-source="[&lt;strong&gt;ClosePort&lt;/strong&gt;](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeport)"><strong>ClosePort</strong></a></p></td>
<td><p>当没有打印机连接到端口时关闭端口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/previous-versions/ff548742(v=vs.85)" data-raw-source="[&lt;strong&gt;EndDocPort&lt;/strong&gt;](/previous-versions/ff548742(v=vs.85))"><strong>EndDocPort</strong></a></p></td>
<td><p>对端口执行打印作业结束任务。</p></td>
</tr>
<tr class="even">
<td><p><a href="/previous-versions/ff550506(v=vs.85)" data-raw-source="[&lt;strong&gt;GetPrinterDataFromPort&lt;/strong&gt;](/previous-versions/ff550506(v=vs.85))"><strong>GetPrinterDataFromPort</strong></a></p></td>
<td><p>可选。 为注册表中存储的值轮询端口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2" data-raw-source="[&lt;strong&gt;InitializePrintMonitor2&lt;/strong&gt;](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2)"><strong>InitializePrintMonitor2</strong></a></p></td>
<td><p>初始化打印监视器并返回实例句柄。</p></td>
</tr>
<tr class="even">
<td><p><a href="/previous-versions/ff559596(v=vs.85)" data-raw-source="[&lt;strong&gt;OpenPortEx&lt;/strong&gt;](/previous-versions/ff559596(v=vs.85))"><strong>OpenPortEx</strong></a></p></td>
<td><p>打开新连接的打印机的端口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/winsplp/nf-winsplp-readport" data-raw-source="[&lt;strong&gt;ReadPort&lt;/strong&gt;](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-readport)"><strong>ReadPort</strong></a></p></td>
<td><p>从打印机端口读取数据。</p></td>
</tr>
<tr class="even">
<td><p><a href="/previous-versions/ff562071(v=vs.85)" data-raw-source="[&lt;strong&gt;SendRecvBidiDataFromPort&lt;/strong&gt;](/previous-versions/ff562071(v=vs.85))"><strong>SendRecvBidiDataFromPort</strong></a></p></td>
<td><p>可选。 支持应用程序与打印机或打印服务器之间的双向通信。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/previous-versions/ff562646(v=vs.85)" data-raw-source="[&lt;strong&gt;Shutdown&lt;/strong&gt;](/previous-versions/ff562646(v=vs.85))"><strong>立即</strong></a></p></td>
<td><p>可选。 删除监视器实例。 此函数对于群集支持是必需的。</p></td>
</tr>
<tr class="even">
<td><p><a href="/previous-versions/ff562710(v=vs.85)" data-raw-source="[&lt;strong&gt;StartDocPort&lt;/strong&gt;](/previous-versions/ff562710(v=vs.85))"><strong>StartDocPort</strong></a></p></td>
<td><p>执行在端口上启动打印作业所需的任务。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/winsplp/nf-winsplp-writeport" data-raw-source="[&lt;strong&gt;WritePort&lt;/strong&gt;](/windows-hardware/drivers/ddi/winsplp/nf-winsplp-writeport)"><strong>WritePort</strong></a></p></td>
<td><p>将数据写入打印机端口。</p></td>
</tr>
</tbody>
</table>

 

