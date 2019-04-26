---
title: IrqlReturn 规则 (wdm)
description: IrqlReturn 规则指定驱动程序的调度例程返回在相同的 IRQL 在其中调用它们。
ms.assetid: 1b2ef432-e3ba-4a01-b3df-839ff13b03f6
ms.date: 05/21/2018
keywords:
- IrqlReturn 规则 (wdm)
topic_type:
- apiref
api_name:
- IrqlReturn
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6440f7c7caa6bae97e1ef49a13532d06b8f56680
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331368"
---
# <a name="irqlreturn-rule-wdm"></a>IrqlReturn 规则 (wdm)


**IrqlReturn**规则指定驱动程序的调度例程返回在相同的 IRQL 在其中调用它们。 有关在的调度例程正确调用于 Irql 详细信息，请参阅[**调度例程和于 Irql。**](https://msdn.microsoft.com/library/windows/hardware/ff544039)

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrqlReturn</strong>规则。</p>
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

<a name="see-also"></a>请参阅
--------

[**调度例程和于 Irql**](https://msdn.microsoft.com/library/windows/hardware/ff544039)
 

 





