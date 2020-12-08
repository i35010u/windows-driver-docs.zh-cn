---
title: WDM 驱动程序的规则
description: WDM 驱动程序的规则
ms.date: 05/21/2018
keywords:
- 静态驱动程序验证程序 WDK，规则
- StaticDV WDK，规则
- SDV WDK，规则
- 规则 WDK 静态驱动程序验证程序
ms.localizationpriority: medium
ms.openlocfilehash: e26945c8dc0928b11ab38bd3b9bf21dfd59332e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815467"
---
# <a name="rules-for-wdm-drivers"></a>WDM 驱动程序的规则


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
<td align="left"><p><a href="default-rule-set--wdm-.md" data-raw-source="[Default rule set (WDM)](default-rule-set--wdm-.md)">默认规则集 (WDM)</a></p></td>
<td align="left"><p>默认 (规则集) 指定在分析驱动程序时要使用的建议的规则集。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddi-usage-rule-set--wdm-.md" data-raw-source="[DDI usage rule set (WDM)](ddi-usage-rule-set--wdm-.md)">DDI 用法规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则验证驱动程序正确使用 WDM DDIs。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="irppending-rule-set--wdm-.md" data-raw-source="[IrpPending rule set (WDM)](irppending-rule-set--wdm-.md)">IrpPending 规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则验证驱动程序是否正确 pends i/o 请求数据包 (IRP) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="irpprocessing-rule-set--wdm-.md" data-raw-source="[IrpProcessing rule set (WDM)](irpprocessing-rule-set--wdm-.md)">IrpProcessing 规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则验证你的驱动程序是否正确处理 (IRP) 的 i/o 请求包。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="irptracking-rule-set--wdm-.md" data-raw-source="[IrpTracking rule set (WDM)](irptracking-rule-set--wdm-.md)">IrpTracking 规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则验证你的驱动程序是否正确跟踪 (IRP) 的 i/o 请求包，以便在完成 Irp 时不删除设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="irql-rule-set--wdm-.md" data-raw-source="[Irql rule set (WDM)](irql-rule-set--wdm-.md)">Irql rule set (WDM)</a></p></td>
<td align="left"><p>使用这些规则验证你的驱动程序是否在所需的 IRQL 上进行 DDI 调用。</p>
<p>不遵循 IRQL 规则的驱动程序可能会导致在操作过程中出现严重问题，从而导致死锁情况或计算机崩溃。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="localirpprocessing-rule-set--wdm-.md" data-raw-source="[LocalIrpProcessing rule set (WDM)](localirpprocessing-rule-set--wdm-.md)">LocalIrpProcessing 规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则验证驱动程序是否正确处理 (IRP) 的驱动程序创建的 i/o 请求包。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="locking-rule-set--wdm-.md" data-raw-source="[Locking rule set (WDM)](locking-rule-set--wdm-.md)">锁定规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则验证驱动程序是否正确管理共享资源。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="miscellaneous-rule-set--wdm-.md" data-raw-source="[Miscellaneous rule set (WDM)](miscellaneous-rule-set--wdm-.md)">其他规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则来验证驱动程序是否正确遵循了对注册表项、字符串和设备对象指针的正确处理的一组一般要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="warning-rule-set--wdm-.md" data-raw-source="[Warning rule set (WDM)](warning-rule-set--wdm-.md)">警告规则集 (WDM)</a></p></td>
<td align="left"><p>使用这些规则来验证驱动程序是否可以在不同的上下文中正确处理 Irp，并遵循 Microsoft 推荐的最佳做法。</p></td>
</tr>
</tbody>
</table>

 

 

 





