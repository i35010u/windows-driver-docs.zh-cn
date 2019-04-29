---
title: 标志\_Irql 规则 (ndis)
description: 标志\_Irql 规则指定 KeGetCurrentIrql 必须不在具有一个调度级别标志参数，指示当前 IRQL 的回调函数内进行调用。
ms.assetid: 19c5c497-9648-4be9-87d1-82f4fa295351
ms.date: 05/21/2018
keywords:
- Flags_Irql 规则 (ndis)
topic_type:
- apiref
api_name:
- Flags_Irql
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cdec7218321d266784d63edb5b6dfcad933bb711
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323814"
---
# <a name="flagsirql-rule-ndis"></a>标志\_Irql 规则 (ndis)


**标志\_Irql**规则指定**KeGetCurrentIrql**不得调用具有一个调度级别标志参数，指示当前 IRQL 的回调函数中。

正确使用调度级别标志可以帮助您避免不必要的尝试设置 IRQL。 有关如何使用此标志的详细信息，请参阅[调度 IRQL 跟踪](https://msdn.microsoft.com/library/windows/hardware/ff546448)。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>Flags_Irql</strong>规则。</p>
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

 

 





