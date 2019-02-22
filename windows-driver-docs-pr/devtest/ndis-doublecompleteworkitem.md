---
title: DoubleCompleteWorkItem 规则 (ndis)
description: DoubleCompleteWorkItem 规则指定，NDIS 驱动程序必须完成的 OID 请求多个时间时完成延迟为工作项中。
ms.assetid: 7add7473-0324-42e9-83bc-8f563410e44f
ms.date: 05/21/2018
keywords:
- DoubleCompleteWorkItem 规则 (ndis)
topic_type:
- apiref
api_name:
- DoubleCompleteWorkItem
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fad1b9bfe13059d53c5337fe8fd37f17c206ba66
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523898"
---
# <a name="doublecompleteworkitem-rule-ndis"></a>DoubleCompleteWorkItem 规则 (ndis)


DoubleCompleteWorkItem 规则指定，NDIS 驱动程序必须完成的 OID 请求多个时间时完成延迟为工作项中。

此规则跟踪 OID 和验证，该驱动程序将工作项排队，当驱动程序不会调用**NdisMOidRequestComplete**多次上相同的 OID。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>DoubleCompleteWorkItem</strong>规则。</p>
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

[**NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)
 

 





