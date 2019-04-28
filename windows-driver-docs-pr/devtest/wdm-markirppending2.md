---
title: MarkIrpPending2 规则 (wdm)
description: MarkIrpPending2 规则指定如果调度例程将返回状态\_挂起状态，它已调用 IoMarkIrpPending 或 IRP 传递到较低的驱动程序。 免费赠送的规范，请参阅 MarkIrpPending。
ms.assetid: 91e22348-f5f3-4ba0-b8dd-ec0aa4b1df5e
ms.date: 05/21/2018
keywords:
- MarkIrpPending2 规则 (wdm)
topic_type:
- apiref
api_name:
- MarkIrpPending2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e47ff85ce9d51b2735401561f96848dd0862b18f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331342"
---
# <a name="markirppending2-rule-wdm"></a>MarkIrpPending2 规则 (wdm)


**MarkIrpPending2**规则指定如果调度例程将返回状态\_挂起状态，该维度被称为[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)或传递到 IRP较低的驱动程序。 请参阅[ **MarkIrpPending** ](wdm-markirppending.md)免费赠送的规范。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>MarkIrpPending2</strong>规则。</p>
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
[**IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)
[**KeWaitForSingleObject**](https://msdn.microsoft.com/library/windows/hardware/ff553350) 
 [ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
[**RemoveHeadList** ](https://msdn.microsoft.com/library/windows/hardware/ff561032)另请参阅
--------

[**MarkIrpPending**](wdm-markirppending.md)
[**同步 IRP 取消**](https://msdn.microsoft.com/library/windows/hardware/ff564531)
 

 





