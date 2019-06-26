---
title: Storport 驱动程序的规则
description: Storport 驱动程序的规则
ms.assetid: C880A30B-8629-4648-B2E3-7AC8F1A9059D
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1f6292d854837d636b5c7e45c7af8be26fec5b44
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378293"
---
# <a name="rules-for-storport-drivers"></a>Storport 驱动程序的规则


本部分列出并描述[DDI 符合性规则](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-rule)Storport 驱动程序可包括在验证您的驱动程序中。

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="default-rule-set--storport-.md" data-raw-source="[Default rule set (Storport)](default-rule-set--storport-.md)">默认规则设置 (Storport)</a></p></td>
<td align="left"><p>默认规则集 (Default.sdv) 指定建议的规则分析您的驱动程序时要使用的集。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddi-usage-rule-set--storport-.md" data-raw-source="[DDI usage rule set (Storport)](ddi-usage-rule-set--storport-.md)">DDI 使用规则集 (Storport)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确使用 Storport DDIs 正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="irql-rule-set--storport-.md" data-raw-source="[Irql rule set (Storport)](irql-rule-set--storport-.md)">Irql 规则集 (Storport)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序所需的 IRQL 在进行 DDI 调用。</p>
<p>未遵循 IRQL 规则的驱动程序可以操作可能会导致死锁条件或计算机崩溃期间导致严重问题。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="locking-rule-set--storport-.md" data-raw-source="[Locking rule set (Storport)](locking-rule-set--storport-.md)">锁定规则集 (Storport)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确管理共享的资源。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="srbprocessing-rule-set--storport-.md" data-raw-source="[SrbProcessing rule set (Storport)](srbprocessing-rule-set--storport-.md)">SrbProcessing 规则集 (Storport)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确处理 SRB 请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="virtualstorport-rule-set--storport-.md" data-raw-source="[VirtualStorport rule set (Storport)](virtualstorport-rule-set--storport-.md)">VirtualStorport 规则集 (Storport)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确调用 DDIs Storport 虚拟微型端口 (VMiniport) 驱动程序特定的感兴趣的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="warning-rule-set--storport-.md" data-raw-source="[Warning rule set (Storport)](warning-rule-set--storport-.md)">警告规则集 (Storport)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序可以正确地处理 Irp，各种上下文中，如下所示，Microsoft 建议的最佳实践。</p></td>
</tr>
</tbody>
</table>

 

 

 





