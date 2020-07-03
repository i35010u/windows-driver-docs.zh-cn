---
title: PagedCode 规则（storport）
description: 此规则验证在 \_ 调用分页代码宏时，驱动程序是否处于 IRQL 调度 \_ 级别。 在 IRQL 调度级别执行的任何代码 \_ 必须位于非分页内存中，以避免导致页错误。
ms.assetid: 7FED3FEF-E6E5-4C26-8777-0A4BCCE0E1EE
ms.date: 05/21/2018
keywords:
- PagedCode 规则（storport）
topic_type:
- apiref
api_name:
- PagedCode
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: daad3c8547dfc9686e558a9d17350b02b981d9a1
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916732"
---
# <a name="pagedcode-rule-storport"></a>PagedCode 规则（storport）


此规则验证在调用[**分页 \_ 代码**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)宏时，驱动程序是否处于**IRQL &lt; 调度 \_ 级别**。 在**IRQL &gt; = 调度 \_ 级别**执行的任何代码必须位于非分页内存中，以避免导致页错误。

**驱动程序模型： Storport**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>PagedCode</strong>规则。</p>
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
 

 





