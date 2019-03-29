---
title: IrpProcessingComplete 规则 (wdm)
description: IrpProcessingComplete 规则指定如果调度例程将返回状态\_成功，IRP 必须已完成任一驱动程序本身或较低级别驱动程序。
ms.assetid: e0dc995e-a5a0-44e3-8cf1-52df8a825598
ms.date: 05/21/2018
keywords:
- IrpProcessingComplete 规则 (wdm)
topic_type:
- apiref
api_name:
- IrpProcessingComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 20498c3898a49a6d43c7707e352344a34c047b78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567583"
---
# <a name="irpprocessingcomplete-rule-wdm"></a>IrpProcessingComplete 规则 (wdm)


**IrpProcessingComplete**规则指定如果调度例程将返回状态\_成功，IRP 必须已完成任一驱动程序本身或较低级别驱动程序。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrpProcessingComplete</strong>规则。</p>
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

[**IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)
[**KeWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff553324) 
 [ **KeWaitForSingleObject**](https://msdn.microsoft.com/library/windows/hardware/ff553350)
[**PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) 
[ **RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)
 

 





