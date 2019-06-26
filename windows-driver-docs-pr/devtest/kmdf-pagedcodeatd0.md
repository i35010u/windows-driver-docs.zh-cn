---
title: PagedCodeAtD0 规则 (kmdf)
description: PagedCodeAtD0 规则指定一个驱动程序必须将标记为可分页的强化代码路径中的回调函数中的代码。
ms.assetid: e3e0ee8f-eebe-4855-be35-3d8b153dd09e
ms.date: 05/21/2018
keywords:
- PagedCodeAtD0 规则 (kmdf)
topic_type:
- apiref
api_name:
- PagedCodeAtD0
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 52981b20ecefd5de443c0da8680cad1a77738082
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392979"
---
# <a name="pagedcodeatd0-rule-kmdf"></a>PagedCodeAtD0 规则 (kmdf)


**PagedCodeAtD0**规则指定一个驱动程序必须将标记为可分页的强化代码路径中的回调函数中的代码。

当一个函数被标记为可分页，在代码部分随后换出时，该函数将生成页面错误，这可能会影响计算机的快速恢复行为。 这是因为客户端驱动程序将需要等待，直到系统驱动程序可以处理此页面错误。

|              |      |
|--------------|------|
| 驱动程序模型 | KMDF |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>PagedCodeAtD0</strong>规则。</p>
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
 

 





