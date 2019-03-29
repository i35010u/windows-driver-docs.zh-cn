---
title: IrqlKeWaitForMultipleObjects 规则 (wdm)
description: IrqlKeWaitForMultipleObjects 规则指定，必须在基于超时参数的正确 IRQL 运行 KeWaitForMultipleObjects 例程的调用方。
ms.assetid: FC3E3544-95FB-4283-B030-66D74D0F7848
ms.date: 05/21/2018
keywords:
- IrqlKeWaitForMultipleObjects 规则 (wdm)
topic_type:
- apiref
api_name:
- IrqlKeWaitForMultipleObjects
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0e55ed355ccb1fbd8abef65a71ad8f0ade1fe4ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568903"
---
# <a name="irqlkewaitformultipleobjects-rule-wdm"></a>IrqlKeWaitForMultipleObjects 规则 (wdm)


**IrqlKeWaitForMultipleObjects**规则指定的调用方[ **KeWaitForMultipleObjects** ](https://msdn.microsoft.com/library/windows/hardware/ff553324)例程必须运行在基于正确IRQL*超时*参数。

调用方**IrqlKeWaitForMultipleObjects**例程可以运行在 IRQL &lt;= 调度\_级别，除在以下情况下：

-   如果*超时* &lt; &gt; 0 的调用方[ **KeWaitForMultipleObjects** ](https://msdn.microsoft.com/library/windows/hardware/ff553324)例程必须运行在 IRQL &lt;= APC\_级别。
-   如果*超时*！ = NULL 并\**超时*= 0 时，调用方[ **KeWaitForMultipleObjects** ](https://msdn.microsoft.com/library/windows/hardware/ff553324)例程必须正在运行在 IRQL = 调度\_级别。

-   如果*超时* = **NULL**，或\**超时*！ = 0 时，调用方的[ **KeWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff553324)例程必须运行在 IRQL &lt;= APC\_级别。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrqlKeWaitForMultipleObjects</strong>规则。</p>
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

[**KeWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff553324)
 

 





