---
title: WDM 驱动程序的规则
description: WDM 驱动程序的规则
ms.assetid: 4e8bc895-4f36-450c-8017-996df482b90d
ms.date: 05/21/2018
keywords:
- 静态驱动程序验证程序 WDK 规则
- StaticDV WDK 规则
- SDV WDK 规则
- 规则 WDK Static Driver Verifier
ms.localizationpriority: medium
ms.openlocfilehash: 83531f9843ad1cafb3dc6d0466b71962e0c893d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340133"
---
# <a name="rules-for-wdm-drivers"></a>WDM 驱动程序的规则


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
<td align="left"><p><a href="default-rule-set--wdm-.md" data-raw-source="[Default rule set (WDM)](default-rule-set--wdm-.md)">默认规则设置 (WDM)</a></p></td>
<td align="left"><p>默认规则集 (Default.sdv) 指定建议的规则分析您的驱动程序时要使用的集。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddi-usage-rule-set--wdm-.md" data-raw-source="[DDI usage rule set (WDM)](ddi-usage-rule-set--wdm-.md)">DDI 使用规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确使用 WDM DDIs 正确。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="irppending-rule-set--wdm-.md" data-raw-source="[IrpPending rule set (WDM)](irppending-rule-set--wdm-.md)">IrpPending 规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确地等待 I/O 请求数据包 (IRP)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="irpprocessing-rule-set--wdm-.md" data-raw-source="[IrpProcessing rule set (WDM)](irpprocessing-rule-set--wdm-.md)">IrpProcessing 规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确处理 I/O 请求数据包 (IRP)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="irptracking-rule-set--wdm-.md" data-raw-source="[IrpTracking rule set (WDM)](irptracking-rule-set--wdm-.md)">IrpTracking 规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确跟踪 I/O 请求数据包 (IRP)，这样，Irp 未完成而不删除该设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="irql-rule-set--wdm-.md" data-raw-source="[Irql rule set (WDM)](irql-rule-set--wdm-.md)">Irql 规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序所需的 IRQL 在进行 DDI 调用。</p>
<p>未遵循 IRQL 规则的驱动程序可以操作可能会导致死锁条件或计算机崩溃期间导致严重问题。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="localirpprocessing-rule-set--wdm-.md" data-raw-source="[LocalIrpProcessing rule set (WDM)](localirpprocessing-rule-set--wdm-.md)">LocalIrpProcessing 规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确地处理 I/O 请求数据包 (IRP) 创建的驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="locking-rule-set--wdm-.md" data-raw-source="[Locking rule set (WDM)](locking-rule-set--wdm-.md)">锁定规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确管理共享的资源。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="miscellaneous-rule-set--wdm-.md" data-raw-source="[Miscellaneous rule set (WDM)](miscellaneous-rule-set--wdm-.md)">其他规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序正确地遵循一组常规的要求正确处理的注册表项、 字符串和设备对象指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="warning-rule-set--wdm-.md" data-raw-source="[Warning rule set (WDM)](warning-rule-set--wdm-.md)">警告规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则来验证您的驱动程序可以正确地处理 Irp，各种上下文中，如下所示，Microsoft 建议的最佳实践。</p></td>
</tr>
</tbody>
</table>

 

 

 





