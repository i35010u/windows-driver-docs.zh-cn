---
title: NDIS 驱动程序的规则
description: NDIS 驱动程序的规则
ms.assetid: fd31b797-1175-4f65-8fa0-a50acd01f446
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 18051a880e7f048efc37ece0e81e62f36cb50362
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526705"
---
# <a name="rules-for-ndis-drivers"></a>NDIS 驱动程序的规则


本部分列出并描述[Static Driver Verifier 规则](https://msdn.microsoft.com/library/windows/hardware/ff552839)可以验证您的驱动程序中包含的 NDIS 驱动程序。

## <a name="in-this-section"></a>本部分内容


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
<td align="left"><p><a href="default-rule-set--ndis-.md" data-raw-source="[Default rule set (NDIS)](default-rule-set--ndis-.md)">默认规则设置 (NDIS)</a></p></td>
<td align="left"><p>默认规则集 (Default.sdv) 指定建议的规则分析您的驱动程序时要使用的集。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddi-usage-rule-set--ndis-.md" data-raw-source="[DDI usage rule set (NDIS)](ddi-usage-rule-set--ndis-.md)">DDI 使用规则集 (NDIS)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确使用 NDIS DDIs 正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="irql-rule-set--ndis-.md" data-raw-source="[IRQL rule set (NDIS)](irql-rule-set--ndis-.md)">IRQL 规则集 (NDIS)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序所需的 IRQL 在进行 DDI 调用。</p>
<p>未遵循 IRQL 规则的驱动程序可以操作可能会导致死锁条件或计算机崩溃期间导致严重问题。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="locking-rule-set--ndis-.md" data-raw-source="[Locking rule set (NDIS)](locking-rule-set--ndis-.md)">锁定规则集 (NDIS)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确管理共享的资源。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="memory-usage-rule-set--ndis-.md" data-raw-source="[Memory usage rule set (NDIS)](memory-usage-rule-set--ndis-.md)">内存使用率规则设置 (NDIS)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确调用 NDIS 函数来分配和释放内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="miscellaneous-rule-set--ndis-.md" data-raw-source="[Miscellaneous rule set (NDIS)](miscellaneous-rule-set--ndis-.md)">其他规则集 (NDIS)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确地遵循一组常规的计时器、 暂停操作、 密钥、 字符串和绑定要求正确处理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="oidprocessing-rule-set--ndis-.md" data-raw-source="[OidProcessing rule set (NDIS)](oidprocessing-rule-set--ndis-.md)">OidProcessing 规则集 (NDIS)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确处理 OID 请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="warning-rule-set--ndis-.md" data-raw-source="[Warning rule set (NDIS)](warning-rule-set--ndis-.md)">警告规则集 (NDIS)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序可以正确地处理 Irp，各种上下文中，如下所示，Microsoft 建议的最佳实践。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-wifi-verification-rule-set.md" data-raw-source="[NDIS/WIFI verification rule set](ndis-wifi-verification-rule-set.md)">NDIS/WIFI 验证规则集</a></p></td>
<td align="left"><blockquote>
[!Note]<br />
可以使用这些规则从 Windows 8.1 开始测试 NDIS/WIFI 驱动程序。
</blockquote>
 </td>
</tr>
</tbody>
</table>

 

 

 





