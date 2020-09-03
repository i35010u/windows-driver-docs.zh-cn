---
title: NDIS 驱动程序的规则
description: NDIS 驱动程序的规则
ms.assetid: fd31b797-1175-4f65-8fa0-a50acd01f446
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: fd8f59801878ca09963f8df46fa7254cb4b31235
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384855"
---
# <a name="rules-for-ndis-drivers"></a>NDIS 驱动程序的规则


本部分列出并描述了可包含在驱动程序验证中的 NDIS 驱动程序的 [静态驱动程序验证程序规则](./static-driver-verifier-rule.md) 。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="default-rule-set--ndis-.md" data-raw-source="[Default rule set (NDIS)](default-rule-set--ndis-.md)">默认规则集 (NDIS)</a></p></td>
<td align="left"><p>默认 (规则集) 指定在分析驱动程序时要使用的建议的规则集。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddi-usage-rule-set--ndis-.md" data-raw-source="[DDI usage rule set (NDIS)](ddi-usage-rule-set--ndis-.md)">DDI 用法规则集 (NDIS)</a></p></td>
<td align="left"><p>使用这些规则验证驱动程序正确使用 NDIS DDIs。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="irql-rule-set--ndis-.md" data-raw-source="[IRQL rule set (NDIS)](irql-rule-set--ndis-.md)">IRQL 规则集 (NDIS)</a></p></td>
<td align="left"><p>使用这些规则验证你的驱动程序是否在所需的 IRQL 上进行 DDI 调用。</p>
<p>不遵循 IRQL 规则的驱动程序可能会导致在操作过程中出现严重问题，从而导致死锁情况或计算机崩溃。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="locking-rule-set--ndis-.md" data-raw-source="[Locking rule set (NDIS)](locking-rule-set--ndis-.md)">锁定规则集 (NDIS)</a></p></td>
<td align="left"><p>使用这些规则验证驱动程序是否正确管理共享资源。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="memory-usage-rule-set--ndis-.md" data-raw-source="[Memory usage rule set (NDIS)](memory-usage-rule-set--ndis-.md)">内存用法规则集 (NDIS)</a></p></td>
<td align="left"><p>使用这些规则验证驱动程序是否正确调用 NDIS 函数以分配和释放内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="miscellaneous-rule-set--ndis-.md" data-raw-source="[Miscellaneous rule set (NDIS)](miscellaneous-rule-set--ndis-.md)">其他规则集 (NDIS)</a></p></td>
<td align="left"><p>使用这些规则来验证驱动程序是否正确遵循了对计时器、暂停操作、键、字符串和绑定的正确处理的一组一般要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="oidprocessing-rule-set--ndis-.md" data-raw-source="[OidProcessing rule set (NDIS)](oidprocessing-rule-set--ndis-.md)">OidProcessing 规则集 (NDIS)</a></p></td>
<td align="left"><p>使用这些规则验证驱动程序是否正确地处理了 OID 请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="warning-rule-set--ndis-.md" data-raw-source="[Warning rule set (NDIS)](warning-rule-set--ndis-.md)">警告规则集 (NDIS)</a></p></td>
<td align="left"><p>使用这些规则来验证驱动程序是否可以在不同的上下文中正确处理 Irp，并遵循 Microsoft 推荐的最佳做法。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wifi-verification-rule-set.md" data-raw-source="[NDIS/WIFI verification rule set](ndis-wifi-verification-rule-set.md)">NDIS/WIFI 验证规则集</a></p></td>
<td align="left"><blockquote>
[!Note]<br />
可以从 Windows 8.1 开始测试 NDIS/WIFI 驱动程序，这些规则从开始。
</blockquote>
 </td>
</tr>
</tbody>
</table>

 

 

