---
title: NdisMIndicateStatusEx 规则（ndis）
description: 驱动程序从 MiniportHaltEx 函数返回后，不能调用 NdisMIndicateStatusEx。
ms.assetid: 488882DB-F294-40A1-BF35-E65262554E11
ms.date: 05/21/2018
keywords:
- NdisMIndicateStatusEx 规则（ndis）
topic_type:
- apiref
api_name:
- NdisMIndicateStatusEx
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 10208ccabc7944762e4d8671ff97a89dc0af2b6a
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917575"
---
# <a name="ndismindicatestatusex-rule-ndis"></a>NdisMIndicateStatusEx 规则（ndis）


驱动程序从[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数返回后，不能调用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) 。

**驱动程序模型： NDIS**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>NdisMIndicateStatusEx</strong>规则。</p>
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

[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)
 

 





