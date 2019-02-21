---
title: SetCompletionRoutineFromDispatch 规则 (kmdf)
description: SetCompletionRoutineFromDispatch 规则验证该驱动程序未指定从其 EvtDeviceWdmIrpDispatch 回调函数 IRP 上完成例程。
ms.assetid: 2D7BA8DC-7288-4DE5-B335-A289C1E995AF
ms.date: 05/21/2018
keywords:
- SetCompletionRoutineFromDispatch 规则 (kmdf)
topic_type:
- apiref
api_name:
- SetCompletionRoutineFromDispatch
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 085ceaad1e2882d3e68981ca8589c413309f66c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526335"
---
# <a name="setcompletionroutinefromdispatch-rule-kmdf"></a>SetCompletionRoutineFromDispatch 规则 (kmdf)


**SetCompletionRoutineFromDispatch**规则将验证该驱动程序未指定完成例程上从 IRP 其[ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)回调函数。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>SetCompletionRoutineFromDispatch</strong>规则。</p>
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

[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)
[**IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
 

 





