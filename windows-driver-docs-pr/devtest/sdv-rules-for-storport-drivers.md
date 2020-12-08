---
title: Storport 驱动程序的规则
description: Storport 驱动程序的规则
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: ea4849fe68d25522339e857baafd020b7cb83472
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838321"
---
# <a name="rules-for-storport-drivers"></a>Storport 驱动程序的规则


本部分列出并描述了可包含在驱动程序验证中的 Storport 驱动程序的 [DDI 符合性规则](./static-driver-verifier-rule.md) 。

## <a name="in-this-section"></a>在本节中


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
<td align="left"><p><a href="default-rule-set--storport-.md" data-raw-source="[Default rule set (Storport)](default-rule-set--storport-.md)">默认规则集 (Storport)</a></p></td>
<td align="left"><p>默认 (规则集) 指定在分析驱动程序时要使用的建议的规则集。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddi-usage-rule-set--storport-.md" data-raw-source="[DDI usage rule set (Storport)](ddi-usage-rule-set--storport-.md)">DDI 用法规则集 (Storport)</a></p></td>
<td align="left"><p>使用这些规则验证驱动程序正确使用 Storport DDIs。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="irql-rule-set--storport-.md" data-raw-source="[Irql rule set (Storport)](irql-rule-set--storport-.md)">Irql 规则集 (Storport)</a></p></td>
<td align="left"><p>使用这些规则验证你的驱动程序是否在所需的 IRQL 上进行 DDI 调用。</p>
<p>不遵循 IRQL 规则的驱动程序可能会导致在操作过程中出现严重问题，从而导致死锁情况或计算机崩溃。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="locking-rule-set--storport-.md" data-raw-source="[Locking rule set (Storport)](locking-rule-set--storport-.md)">锁定规则集 (Storport)</a></p></td>
<td align="left"><p>使用这些规则验证驱动程序是否正确管理共享资源。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="srbprocessing-rule-set--storport-.md" data-raw-source="[SrbProcessing rule set (Storport)](srbprocessing-rule-set--storport-.md)">SrbProcessing 规则集 (Storport)</a></p></td>
<td align="left"><p>使用这些规则验证驱动程序是否正确地处理 SRB 请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="virtualstorport-rule-set--storport-.md" data-raw-source="[VirtualStorport rule set (Storport)](virtualstorport-rule-set--storport-.md)">VirtualStorport 规则集 (Storport)</a></p></td>
<td align="left"><p>使用这些规则验证你的驱动程序是否正确地调用 (VMiniport) 驱动程序的 Storport 虚拟小型端口。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="warning-rule-set--storport-.md" data-raw-source="[Warning rule set (Storport)](warning-rule-set--storport-.md)">警告规则集 (Storport)</a></p></td>
<td align="left"><p>使用这些规则来验证驱动程序是否可以在不同的上下文中正确处理 Irp，并遵循 Microsoft 推荐的最佳做法。</p></td>
</tr>
</tbody>
</table>

 

 

