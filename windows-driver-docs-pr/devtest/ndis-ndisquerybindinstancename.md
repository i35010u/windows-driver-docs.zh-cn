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
ms.openlocfilehash: c54206591494385e242a1116baf516a0bdc25493
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354367"
---
# <a name="ndisquerybindinstancename-rule-ndis"></a>NdisQueryBindInstanceName 规则 (ndis)


[**NdisQueryBindInstanceName** ](https://msdn.microsoft.com/library/windows/hardware/ff563748)为指定的友好名称的字符串分配内存。 调用方完成使用此内存后，必须调用调用方[ **NdisFreeMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff562577)函数，以释放内存。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>NdisQueryBindInstanceName</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**NdisFreeMemory**](https://msdn.microsoft.com/library/windows/hardware/ff562577)
[**NdisQueryBindInstanceName**](https://msdn.microsoft.com/library/windows/hardware/ff563748)
 

 





