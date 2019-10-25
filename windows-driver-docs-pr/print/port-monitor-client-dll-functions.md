---
title: 端口监视器客户端 DLL 函数
description: 端口监视器客户端 DLL 函数
ms.assetid: 41efab1a-0638-4925-90a2-cf68d2306ca6
keywords:
- 端口监视 WDK 打印、功能
- 客户端 DLL 端口监视器函数 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f84669e4662d754b56f2c8ec7676f3ce0dd5a3a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844660"
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
<td><p>DLL 入口点，通常称为<strong>DllMain</strong>，如 Microsoft Windows SDK 文档中所述。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-addportui" data-raw-source="[&lt;strong&gt;AddPortUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-addportui)"><strong>AddPortUI</strong></a></p></td>
<td><p>通过显示一个对话框来创建端口并获取配置信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-configureportui" data-raw-source="[&lt;strong&gt;ConfigurePortUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-configureportui)"><strong>ConfigurePortUI</strong></a></p></td>
<td><p>配置先前添加的端口。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-deleteportui" data-raw-source="[&lt;strong&gt;DeletePortUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-deleteportui)"><strong>DeletePortUI</strong></a></p></td>
<td><p>删除端口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitorui" data-raw-source="[&lt;strong&gt;InitializePrintMonitorUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitorui)"><strong>InitializePrintMonitorUI</strong></a></p></td>
<td><p>初始化端口监视器 UI DLL。</p></td>
</tr>
</tbody>
</table>

 

 

 




