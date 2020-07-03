---
title: PagedCodeAtPowerTrans 规则（wdm）
description: PagedCodeAtPowerTrans 规则指定驱动程序 \_ 在响应系统 irp \_ Mj \_ POWER irp （irp \_ MN \_ 设置 \_ 电源）和设备 IRP \_ mj \_ power irp （irp \_ MN \_ 设置 \_ 电源）时不应调用分页代码。
ms.assetid: D94B0E13-9640-4FBF-B1E7-AF8DFED42542
ms.date: 05/21/2018
keywords:
- PagedCodeAtPowerTrans 规则（wdm）
topic_type:
- apiref
api_name:
- PagedCodeAtPowerTrans
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8f7c991d0f730f5a19ec03394a062079eca39d98
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917701"
---
# <a name="pagedcodeatpowertrans-rule-wdm"></a>PagedCodeAtPowerTrans 规则（wdm）


**PagedCodeAtPowerTrans**规则指定驱动程序在响应系统 irp Mj [** \_ **](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) \_ \_ power irp （IRP \_ MN \_ 设置 \_ 电源）和设备 IRP \_ mj \_ Power irp （irp \_ MN \_ 设置 \_ 电源）时不应调用分页代码。

**驱动程序模型： WDM**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>PagedCodeAtPowerTrans</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**分页 \_ 代码**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)
 

 





