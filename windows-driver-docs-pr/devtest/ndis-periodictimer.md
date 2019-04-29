---
title: PeriodicTimer 规则 (ndis)
description: PeriodicTimer 规则指定 NdisCancelTimerObject 的调用方，必须运行在 IRQL 被动\_级别如果 NdisSetTimerObject 函数的 MillisecondsPeriod 参数中指定了一个非零值。
ms.assetid: a6bda698-5150-4fd5-b665-d460b88fe0ac
ms.date: 05/21/2018
keywords:
- PeriodicTimer 规则 (ndis)
topic_type:
- apiref
api_name:
- PeriodicTimer
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 27d83173e1ce4e77c338156626bccd91e5e8c89b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354347"
---
# <a name="periodictimer-rule-ndis"></a>PeriodicTimer 规则 (ndis)


**PeriodicTimer**规则指定的调用方[ **NdisCancelTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561624)必须在运行**IRQL = 被动\_级别**如果在指定了一个非零值*MillisecondsPeriod*参数[ **NdisSetTimerObject** ](https://msdn.microsoft.com/library/windows/hardware/ff564563)函数。 如果*MillisecondsPeriod*的参数**NdisSetTimerObject**函数是零的调用方**NdisCancelTimerObject**可以在运行**IRQL&lt;= 调度\_级别**。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>PeriodicTimer</strong>规则。</p>
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

[**NdisCancelTimerObject**](https://msdn.microsoft.com/library/windows/hardware/ff561624)
[**NdisSetTimerObject**](https://msdn.microsoft.com/library/windows/hardware/ff564563)
 

 





