---
title: IrqlKeRaiseLower 规则 (wdm)
description: IrqlKeRaiseLower 规则指定驱动程序时提高和降低 IRQL 时驱动程序调用 KeRaiseIrql 执行以下、 低于或等于 NewIrql 参数的值的 IRQL 在正在执行它。该驱动程序仅在调用 KeRaiseIrql 或 KeRaiseIrqlToDpcLevel 后调用 KeLowerIrql。
ms.assetid: 61f7e5bc-ccc5-4ee6-a580-9935a01f96e6
ms.date: 05/21/2018
keywords:
- IrqlKeRaiseLower 规则 (wdm)
topic_type:
- apiref
api_name:
- IrqlKeRaiseLower
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ca77b426cdf58c0c34ec7c818e43094fa0ea0e15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525109"
---
# <a name="irqlkeraiselower-rule-wdm"></a>IrqlKeRaiseLower 规则 (wdm)


**IrqlKeRaiseLower**规则指定驱动程序执行以下操作时提高和降低 IRQL:

当驱动程序调用[ **KeRaiseIrql**](https://msdn.microsoft.com/library/windows/hardware/ff553079)，它是在低于 IRQL 正在执行或等于的值*NewIrql*参数。
驱动程序调用[ **KeLowerIrql** ](https://msdn.microsoft.com/library/windows/hardware/ff552968)仅在调用**KeRaiseIrql**或者[ **KeRaiseIrqlToDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff553084).
此规则将允许嵌套的调用**KeRaiseIrql**， **KeRaiseIrqlToDpcLevel**，并**KeLowerIrql**。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrqlKeRaiseLower</strong>规则。</p>
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

[**KeLowerIrql**](https://msdn.microsoft.com/library/windows/hardware/ff552968)
[**KeRaiseIrql** ](https://msdn.microsoft.com/library/windows/hardware/ff553079)另请参阅
--------

[**IrqlKeDispatchLte**](wdm-irqlkedispatchlte.md)
[**IrqlKeRaiseLower2**](wdm-irqlkeraiselower2.md)
 

 





