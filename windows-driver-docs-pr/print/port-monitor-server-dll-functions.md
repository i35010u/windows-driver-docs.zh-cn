---
title: 端口监视器服务器 DLL 函数
description: 端口监视器服务器 DLL 函数
ms.assetid: ffbcaaaa-7f9d-4b29-b939-189e10174074
keywords:
- 端口监视 WDK 打印、功能
- 服务器 DLL 端口监视器函数 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe80c20139b5b116cd69fb9a3519a0f47391e1e1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842350"
---
# <a name="port-monitor-server-dll-functions"></a>端口监视器服务器 DLL 函数





下表列出了端口监视器服务器 DLL 必须定义的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DllEntryPoint</strong></p></td>
<td><p>DLL 入口点，通常称为<strong>DllMain</strong>，如 Microsoft Windows SDK 文档中所述。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeport" data-raw-source="[&lt;strong&gt;ClosePort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeport)"><strong>ClosePort</strong></a></p></td>
<td><p>如果没有打印机连接到某个端口，则关闭该端口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff548742(v=vs.85)" data-raw-source="[&lt;strong&gt;EndDocPort&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff548742(v=vs.85))"><strong>EndDocPort</strong></a></p></td>
<td><p>对端口执行打印作业结束任务。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff548754(v=vs.85)" data-raw-source="[&lt;strong&gt;EnumPorts&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff548754(v=vs.85))"><strong>EnumPorts</strong></a></p></td>
<td><p>枚举可用于在服务器上打印的端口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2" data-raw-source="[&lt;strong&gt;InitializePrintMonitor2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2)"><strong>InitializePrintMonitor2</strong></a></p></td>
<td><p>初始化打印监视器并返回实例句柄。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openport" data-raw-source="[&lt;strong&gt;OpenPort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openport)"><strong>OpenPort</strong></a></p></td>
<td><p>打开打印机端口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff559596(v=vs.85)" data-raw-source="[&lt;strong&gt;OpenPortEx&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff559596(v=vs.85))"><strong>OpenPortEx</strong></a></p></td>
<td><p>打开打印机端口。 （仅限语言监视器）</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-readport" data-raw-source="[&lt;strong&gt;ReadPort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-readport)"><strong>ReadPort</strong></a></p></td>
<td><p>从打印机端口读取数据。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff562710(v=vs.85)" data-raw-source="[&lt;strong&gt;StartDocPort&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff562710(v=vs.85))"><strong>StartDocPort</strong></a></p></td>
<td><p>执行在端口上启动打印作业所需的任务。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-writeport" data-raw-source="[&lt;strong&gt;WritePort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-writeport)"><strong>WritePort</strong></a></p></td>
<td><p>将数据写入打印机端口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvcloseport" data-raw-source="[&lt;strong&gt;XcvClosePort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvcloseport)"><strong>XcvClosePort</strong></a></p></td>
<td><p>端口管理完成后关闭端口。 适用于 Windows 2000 和更高版本的基于 NT 的操作系统版本。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvdataport" data-raw-source="[&lt;strong&gt;XcvDataPort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvdataport)"><strong>XcvDataPort</strong></a></p></td>
<td><p>处理端口管理任务。 适用于 Windows 2000 和更高版本的基于 NT 的操作系统版本。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvopenport" data-raw-source="[&lt;strong&gt;XcvOpenPort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvopenport)"><strong>XcvOpenPort</strong></a></p></td>
<td><p>出于管理目的打开端口。 适用于 Windows 2000 和更高版本的基于 NT 的操作系统版本。</p></td>
</tr>
</tbody>
</table>

 

以下端口监视器服务器 DLL 函数是可选的。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff550506(v=vs.85)" data-raw-source="[&lt;strong&gt;GetPrinterDataFromPort&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff550506(v=vs.85))"><strong>GetPrinterDataFromPort</strong></a></p></td>
<td><p>将 i/o 控制代码发送到端口驱动程序并返回结果。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff562071(v=vs.85)" data-raw-source="[&lt;strong&gt;SendRecvBidiDataFromPort&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff562071(v=vs.85))"><strong>SendRecvBidiDataFromPort</strong></a></p></td>
<td><p>支持应用程序与打印机或打印服务器之间的双向通信。 在 Windows XP 和更高版本中可用。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff562630(v=vs.85)" data-raw-source="[&lt;strong&gt;SetPortTimeOuts&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff562630(v=vs.85))"><strong>SetPortTimeOuts</strong></a></p></td>
<td><p>在打开的端口上设置超时值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff562646(v=vs.85)" data-raw-source="[&lt;strong&gt;Shutdown&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff562646(v=vs.85))"><strong>立即</strong></a></p></td>
<td><p>删除监视器实例。 此函数对于群集支持是必需的。</p></td>
</tr>
</tbody>
</table>

 

 

 




