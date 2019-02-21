---
title: IrqlExFree3 规则 (wdm)
description: IrqlExFree3 规则指定适当的 IRQL 在调用 ExFreePool 和 ExFreePoolWithTag。
ms.assetid: D3916378-2032-4575-941F-F1EA9A3678F8
ms.date: 05/21/2018
keywords:
- IrqlExFree3 规则 (wdm)
topic_type:
- apiref
api_name:
- IrqlExFree3
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4a3926ec128506ebef662d976aaf5cb0a808e407
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544438"
---
# <a name="irqlexfree3-rule-wdm"></a>IrqlExFree3 规则 (wdm)


**IrqlExFree3**规则指定[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590)并[ **ExFreePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544593)称为在适当的 irql 下完成。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrqlExFree3</strong>规则。</p>
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

[**ExFreePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544593)
 

 





