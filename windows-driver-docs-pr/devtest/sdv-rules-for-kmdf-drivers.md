---
title: KMDF 驱动程序的规则
description: KMDF 驱动程序的规则
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 93b475a7ea8d9d330112d978b99de112eefc629c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838325"
---
# <a name="rules-for-kmdf-drivers"></a>KMDF 驱动程序的规则


本部分列出并描述了可在验证中包含的内核模式驱动程序框架 (KMDF) 驱动程序的 [DDI 符合性规则](static-driver-verifier-rules.md) 。

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
<td align="left"><p><a href="default-rule-set--kmdf-.md" data-raw-source="[Default rule set (KMDF)](default-rule-set--kmdf-.md)">默认规则集 (KMDF)</a></p></td>
<td align="left"><p>默认 (规则集) 指定在分析驱动程序时要使用的建议的规则集。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddi-usage-rule-set--kmdf-.md" data-raw-source="[DDI usage rule set (KMDF)](ddi-usage-rule-set--kmdf-.md)">DDI 用法规则集 (KMDF)</a></p></td>
<td align="left"><p>使用这些规则验证驱动程序是否正确地使用了 KMDF DDIs。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="irpprocessing-rule-set--kmdf-.md" data-raw-source="[IrpProcessing rule set (KMDF)](irpprocessing-rule-set--kmdf-.md)">IrpProcessing 规则集 (KMDF)</a></p></td>
<td align="left"><p>使用这些规则验证你的驱动程序是否正确处理 (IRP) 的 i/o 请求包。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="irql-rule-set--kmdf-.md" data-raw-source="[Irql rule set (KMDF)](irql-rule-set--kmdf-.md)">Irql 规则集 (KMDF)</a></p></td>
<td align="left"><p>使用这些规则验证你的驱动程序是否在所需的 IRQL 上进行 DDI 调用。</p>
<p>不遵循 IRQL 规则的驱动程序可能会导致在操作过程中出现严重问题，从而导致死锁情况或计算机崩溃。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="locking-rule-set--kmdf-.md" data-raw-source="[Locking rule set (KMDF)](locking-rule-set--kmdf-.md)">锁定规则集 (KMDF)</a></p></td>
<td align="left"><p>使用这些规则验证驱动程序是否正确管理共享资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="miscellaneous-rule-set--kmdf-.md" data-raw-source="[Miscellaneous rule set (KMDF)](miscellaneous-rule-set--kmdf-.md)">其他规则集 (KMDF)</a></p></td>
<td align="left"><p>使用这些规则来验证驱动程序是否正确地遵循了对设备对象、密钥的正确处理的一般要求，以及该驱动程序不会对非 PnP 驱动程序或不是电源策略所有者的非 FDO 驱动程序调用 DDIs。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="requestprocessing-rule-set--kmdf-.md" data-raw-source="[RequestProcessing rule set (KMDF)](requestprocessing-rule-set--kmdf-.md)">RequestProcessing 规则集 (KMDF)</a></p></td>
<td align="left"><p>使用这些规则验证驱动程序是否正确完成或取消 (IRP) 的 i/o 请求包。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="usb-rule-set--kmdf-.md" data-raw-source="[Usb rule set (KMDF)](usb-rule-set--kmdf-.md)">USB 规则集 (KMDF)</a></p></td>
<td align="left"><p>使用这些规则验证驱动程序是否正确处理 USB 设备的一些专用 KMDF 方法。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="warning-rule-set--kmdf-.md" data-raw-source="[Warning rule set (KMDF)](warning-rule-set--kmdf-.md)">警告规则集 (KMDF)</a></p></td>
<td align="left"><p>使用这些规则来验证驱动程序是否可以在不同的上下文中正确处理 Irp，并遵循 Microsoft 推荐的最佳做法。</p></td>
</tr>
</tbody>
</table>

 

 

 





