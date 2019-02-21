---
title: 用于 KMDF 驱动程序的规则
description: 用于 KMDF 驱动程序的规则
ms.assetid: 63ac4df5-b2dc-43da-abaa-49c5de036d79
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 91900f908a3d6361c136f1b3a621753d2cee1668
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540644"
---
# <a name="rules-for-kmdf-drivers"></a>用于 KMDF 驱动程序的规则


本部分列出并描述[DDI 符合性规则](static-driver-verifier-rules.md)可包括在验证中的内核模式驱动程序框架 (KMDF) 驱动程序。

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
<td align="left"><p><a href="default-rule-set--kmdf-.md" data-raw-source="[Default rule set (KMDF)](default-rule-set--kmdf-.md)">默认规则设置 (KMDF)</a></p></td>
<td align="left"><p>默认规则集 (Default.sdv) 指定建议的规则分析您的驱动程序时要使用的集。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddi-usage-rule-set--kmdf-.md" data-raw-source="[DDI usage rule set (KMDF)](ddi-usage-rule-set--kmdf-.md)">DDI 使用规则集 (KMDF)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确使用 KMDF DDIs 正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="irpprocessing-rule-set--kmdf-.md" data-raw-source="[IrpProcessing rule set (KMDF)](irpprocessing-rule-set--kmdf-.md)">IrpProcessing 规则集 (KMDF)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确处理 I/O 请求数据包 (IRP)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="irql-rule-set--kmdf-.md" data-raw-source="[Irql rule set (KMDF)](irql-rule-set--kmdf-.md)">Irql 规则集 (KMDF)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序所需的 IRQL 在进行 DDI 调用。</p>
<p>未遵循 IRQL 规则的驱动程序可以操作可能会导致死锁条件或计算机崩溃期间导致严重问题。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="locking-rule-set--kmdf-.md" data-raw-source="[Locking rule set (KMDF)](locking-rule-set--kmdf-.md)">锁定规则集 (KMDF)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确管理共享的资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="miscellaneous-rule-set--kmdf-.md" data-raw-source="[Miscellaneous rule set (KMDF)](miscellaneous-rule-set--kmdf-.md)">其他规则集 (KMDF)</a></p></td>
<td align="left"><p>使用这些规则，以验证您的驱动程序正确地遵循一组常规设备的要求正确处理对象时，密钥和驱动程序执行不进行调用到 DDIs 不适合非 PnP 驱动程序或不是采购订单的非 FDO 驱动程序wer 策略所有者。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="requestprocessing-rule-set--kmdf-.md" data-raw-source="[RequestProcessing rule set (KMDF)](requestprocessing-rule-set--kmdf-.md)">RequestProcessing 规则集 (KMDF)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确完成或取消 I/O 请求数据包 (IRP)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="usb-rule-set--kmdf-.md" data-raw-source="[Usb rule set (KMDF)](usb-rule-set--kmdf-.md)">Usb 规则集 (KMDF)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确地处理 USB 设备的某些专用的 KMDF 方法。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="warning-rule-set--kmdf-.md" data-raw-source="[Warning rule set (KMDF)](warning-rule-set--kmdf-.md)">警告规则集 (KMDF)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序可以正确地处理 Irp，各种上下文中，如下所示，Microsoft 建议的最佳实践。</p></td>
</tr>
</tbody>
</table>

 

 

 





