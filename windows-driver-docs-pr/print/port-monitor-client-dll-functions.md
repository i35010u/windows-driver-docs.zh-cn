---
title: 端口监视器客户端 DLL 函数
description: 端口监视器客户端 DLL 函数
ms.assetid: 41efab1a-0638-4925-90a2-cf68d2306ca6
keywords:
- 端口监视 WDK 打印函数
- 客户端 DLL 端口监视器功能 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 345f5472f0a9a29301edb7eead6ab534069f9c52
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368975"
---
# <a name="port-monitor-client-dll-functions"></a>端口监视器客户端 DLL 函数





下表列出了端口监视器 UI DLL 必须定义的函数。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-addportui" data-raw-source="[&lt;strong&gt;AddPortUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-addportui)"><strong>AddPortUI</strong></a></p></td>
<td><p>将创建一个端口，并通过显示一个对话框来获取配置信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-configureportui" data-raw-source="[&lt;strong&gt;ConfigurePortUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-configureportui)"><strong>ConfigurePortUI</strong></a></p></td>
<td><p>配置以前添加的端口。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-deleteportui" data-raw-source="[&lt;strong&gt;DeletePortUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-deleteportui)"><strong>DeletePortUI</strong></a></p></td>
<td><p>删除一个端口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-initializeprintmonitorui" data-raw-source="[&lt;strong&gt;InitializePrintMonitorUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-initializeprintmonitorui)"><strong>InitializePrintMonitorUI</strong></a></p></td>
<td><p>初始化端口监视器 UI DLL。</p></td>
</tr>
</tbody>
</table>

 

 

 




