---
title: PagedCodeAtPowerTrans 规则 (wdm)
description: PagedCodeAtPowerTrans 规则指定一个驱动程序不应调用 PAGED\_代码，同时响应系统 IRP\_MJ\_POWER Irp (IRP\_MN\_设置\_POWER) 和设备 IRP\_MJ\_POWER Irp (IRP\_MN\_设置\_电源)。
ms.assetid: D94B0E13-9640-4FBF-B1E7-AF8DFED42542
ms.date: 05/21/2018
keywords:
- PagedCodeAtPowerTrans 规则 (wdm)
topic_type:
- apiref
api_name:
- PagedCodeAtPowerTrans
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 699616ff3c06fcbc4ae11f4d38006a547c05c504
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393709"
---
# <a name="pagedcodeatpowertrans-rule-wdm"></a>PagedCodeAtPowerTrans 规则 (wdm)


**PagedCodeAtPowerTrans**规则指定一个驱动程序不应调用[ **PAGED\_代码**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)时响应系统 IRP\_MJ\_POWER Irp (IRP\_MN\_设置\_电源) 到设备 IRP\_MJ\_POWER Irp (IRP\_MN\_设置\_电源)。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>PagedCodeAtPowerTrans</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**PAGED\_CODE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)
 

 





