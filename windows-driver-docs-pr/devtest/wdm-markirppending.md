---
title: MarkIrpPending 规则 (wdm)
description: MarkIrpPending 规则指定只要调用驱动程序调度例程，该驱动程序返回状态\_挂起的调度例程时结束。 免费赠送的规范，请参阅 MarkIrpPending2。
ms.assetid: cbf5484e-2806-4df6-bdfb-98acfe5d214c
ms.date: 05/21/2018
keywords:
- MarkIrpPending 规则 (wdm)
topic_type:
- apiref
api_name:
- MarkIrpPending
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 981c2e94e486e027571af0b924a6fdd8f717d765
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331345"
---
# <a name="markirppending-rule-wdm"></a>MarkIrpPending 规则 (wdm)


**MarkIrpPending**规则指定只要，驱动程序调度例程调用[ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)，驱动程序将返回状态\_挂起时结束调度例程。 请参阅[ **MarkIrpPending2** ](wdm-markirppending2.md)免费赠送的规范。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>MarkIrpPending</strong>规则。</p>
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
[**IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)
 [ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
[**RemoveHeadList** ](https://msdn.microsoft.com/library/windows/hardware/ff561032)另请参阅
--------

[**MarkingInterlockedQueuedIrps**](wdm-markinginterlockedqueuedirps.md)
[**同步 IRP 取消**](https://msdn.microsoft.com/library/windows/hardware/ff564531)
 

 





