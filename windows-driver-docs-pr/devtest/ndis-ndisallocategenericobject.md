---
title: NdisAllocateGenericObject 规则 (ndis)
description: NdisAllocateGenericObject 规则指定备用的顺序调用 NdisAllocateGenericObject 和 NdisFreeGenericObject。 最终目标是确保 MiniportHaltEx 结束时释放所有泛型对象。
ms.assetid: A247B43F-1958-4A57-AA60-37C995A96DF7
ms.date: 05/21/2018
keywords:
- NdisAllocateGenericObject 规则 (ndis)
topic_type:
- apiref
api_name:
- NdisAllocateGenericObject
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e6549eef3709f64b0e87e1d5fb0c17b3aa0fc19f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526222"
---
# <a name="ndisallocategenericobject-rule-ndis"></a>NdisAllocateGenericObject 规则 (ndis)


**NdisAllocateGenericObject**规则指定[ **NdisAllocateGenericObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561603)并[ **NdisFreeGenericObject**](https://msdn.microsoft.com/library/windows/hardware/ff561850)备用顺序调用。 最终目标是确保所有泛型对象也将释放时[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)结束。

此规则使用三个不同的状态。 状态更改时分配或释放 NDIS 泛型对象。 如果 NDIS 泛型对象仍分配何时[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)退出，该规则将失败。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>NdisAllocateGenericObject</strong>规则。</p>
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

<a name="applies-to"></a>适用于
----------

[**NdisAllocateGenericObject**](https://msdn.microsoft.com/library/windows/hardware/ff561603)
[**NdisFreeGenericObject**](https://msdn.microsoft.com/library/windows/hardware/ff561850)
 

 





