---
title: NdisQueryBindInstanceName 规则 (ndis)
description: NdisQueryBindInstanceName 为指定的友好名称的字符串分配内存。 调用方完成使用此内存后，调用方必须调用 NdisFreeMemory 函数，以释放内存。
ms.assetid: C332698F-8DA5-4A9A-AF2E-5D8B43815488
ms.date: 05/21/2018
keywords:
- NdisQueryBindInstanceName 规则 (ndis)
topic_type:
- apiref
api_name:
- NdisQueryBindInstanceName
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fdd7c6ee4bfa2b4ce03f2d4be7b520c9e00dc9e6
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392211"
---
# <a name="ndisquerybindinstancename-rule-ndis"></a>NdisQueryBindInstanceName 规则 (ndis)


[**NdisQueryBindInstanceName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisquerybindinstancename)为指定的友好名称的字符串分配内存。 调用方完成使用此内存后，必须调用调用方[ **NdisFreeMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreememory)函数，以释放内存。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>NdisQueryBindInstanceName</strong>规则。</p>
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

[**NdisFreeMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreememory)
[**NdisQueryBindInstanceName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisquerybindinstancename)
 

 





