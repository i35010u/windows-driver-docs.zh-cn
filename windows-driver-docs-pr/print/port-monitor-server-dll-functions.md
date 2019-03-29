---
title: 端口监视器服务器 DLL 函数
description: 端口监视器服务器 DLL 函数
ms.assetid: ffbcaaaa-7f9d-4b29-b939-189e10174074
keywords:
- 端口监视 WDK 打印函数
- 服务器 DLL 端口监视器功能 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1723b67b82c0b63321d575c0a865e21eccaf21cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575436"
---
# <a name="port-monitor-server-dll-functions"></a>端口监视器服务器 DLL 函数





下表列出了端口监视服务器 DLL 必须定义的函数。

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
<td><p>DLL 入口点，通常称为<strong>DllMain</strong>，Microsoft Windows SDK 文档中所述。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545975" data-raw-source="[&lt;strong&gt;ClosePort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545975)"><strong>ClosePort</strong></a></p></td>
<td><p>如果不有任何打印机连接到它，请关闭端口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548742" data-raw-source="[&lt;strong&gt;EndDocPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548742)"><strong>EndDocPort</strong></a></p></td>
<td><p>在端口上执行最终的打印作业的任务。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548754" data-raw-source="[&lt;strong&gt;EnumPorts&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548754)"><strong>EnumPorts</strong></a></p></td>
<td><p>枚举可用于打印服务器上的端口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551605" data-raw-source="[&lt;strong&gt;InitializePrintMonitor2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551605)"><strong>InitializePrintMonitor2</strong></a></p></td>
<td><p>初始化的打印监视器并返回一个实例句柄。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559593" data-raw-source="[&lt;strong&gt;OpenPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559593)"><strong>OpenPort</strong></a></p></td>
<td><p>将打开打印机端口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559596" data-raw-source="[&lt;strong&gt;OpenPortEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559596)"><strong>OpenPortEx</strong></a></p></td>
<td><p>将打开打印机端口。 （仅语言监视器）</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561909" data-raw-source="[&lt;strong&gt;ReadPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561909)"><strong>ReadPort</strong></a></p></td>
<td><p>从打印机端口读取数据。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562710" data-raw-source="[&lt;strong&gt;StartDocPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562710)"><strong>StartDocPort</strong></a></p></td>
<td><p>执行所需端口上启动打印作业的任务。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563792" data-raw-source="[&lt;strong&gt;WritePort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563792)"><strong>WritePort</strong></a></p></td>
<td><p>将数据写入到的打印机端口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564254" data-raw-source="[&lt;strong&gt;XcvClosePort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564254)"><strong>XcvClosePort</strong></a></p></td>
<td><p>端口管理完成后，请关闭端口。 在 Windows 2000 和更高版本的基于 NT 的操作系统版本中可用。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564258" data-raw-source="[&lt;strong&gt;XcvDataPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564258)"><strong>XcvDataPort</strong></a></p></td>
<td><p>处理端口的管理任务。 在 Windows 2000 和更高版本的基于 NT 的操作系统版本中可用。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564259" data-raw-source="[&lt;strong&gt;XcvOpenPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564259)"><strong>XcvOpenPort</strong></a></p></td>
<td><p>将打开以进行管理的端口。 在 Windows 2000 和更高版本的基于 NT 的操作系统版本中可用。</p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550506" data-raw-source="[&lt;strong&gt;GetPrinterDataFromPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550506)"><strong>GetPrinterDataFromPort</strong></a></p></td>
<td><p>将 I/O 控制代码发送到端口驱动程序，并返回结果。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562071" data-raw-source="[&lt;strong&gt;SendRecvBidiDataFromPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562071)"><strong>SendRecvBidiDataFromPort</strong></a></p></td>
<td><p>支持应用程序和打印机或打印服务器之间的双向通信。 可在 Windows XP 及更高版本。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562630" data-raw-source="[&lt;strong&gt;SetPortTimeOuts&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562630)"><strong>SetPortTimeOuts</strong></a></p></td>
<td><p>在打开的端口上设置超时值。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562646" data-raw-source="[&lt;strong&gt;Shutdown&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562646)"><strong>Shutdown</strong></a></p></td>
<td><p>删除监视实例。 此函数是必需的群集支持。</p></td>
</tr>
</tbody>
</table>

 

 

 




