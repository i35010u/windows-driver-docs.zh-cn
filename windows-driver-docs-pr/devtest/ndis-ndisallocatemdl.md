---
title: NdisAllocateMdl 规则 (ndis)
description: NdisAllocateMdl 规则指定备用的顺序调用 NdisAllocateMdl 和 NdisFreeMdl。 最终目标是确保所有 MDLs MiniportHaltEx 结束时都释放。
ms.assetid: 8146E72B-0B63-4224-9677-5E6FEFCEB745
ms.date: 05/21/2018
keywords:
- NdisAllocateMdl 规则 (ndis)
topic_type:
- apiref
api_name:
- NdisAllocateMdl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bddec8bb956862bb633611b68732a32a6345bd19
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546561"
---
# <a name="ndisallocatemdl-rule-ndis"></a>NdisAllocateMdl 规则 (ndis)


**NdisAllocateMdl**规则指定[ **NdisAllocateMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff561605)并[ **NdisFreeMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff562575)是备用顺序调用。 最终目标是确保所有 MDLs 时释放[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)结束。

此规则使用三个不同的状态。 状态更改时分配或释放 MDL 时。 如果 MDL 仍分配何时[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)退出，此规则报告缺陷。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>NdisAllocateMdl</strong>规则。</p>
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

[**NdisAllocateMdl**](https://msdn.microsoft.com/library/windows/hardware/ff561605)
[**NdisFreeMdl**](https://msdn.microsoft.com/library/windows/hardware/ff562575)
 

 





