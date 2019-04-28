---
title: LowerDriverReturn 规则 (wdm)
description: LowerDriverReturn 规则指定后使用 PoCallDriver 或 IoCallDriver 调用较低的驱动程序，该驱动程序只有保存从调用返回的状态，并将它收到的返回状态传递到调度例程。
ms.assetid: 0b437591-c613-481a-a4f9-36a5cc208cb0
ms.date: 05/21/2018
keywords:
- LowerDriverReturn 规则 (wdm)
topic_type:
- apiref
api_name:
- LowerDriverReturn
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 14c44a6577aad59822f1fb221f9e1ca65d3ce8ad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331352"
---
# <a name="lowerdriverreturn-rule-wdm"></a>LowerDriverReturn 规则 (wdm)


**LowerDriverReturn**规则指定后使用[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654)或者[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)若要调用的较低的驱动程序，该驱动程序将返回状态保存从调用，并将它收到的返回状态传递到调度例程。

如果该驱动程序调用不会应用这些条件[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)或[ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>LowerDriverReturn</strong>规则。</p>
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
[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679) 
 [ **IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**IoSetDeviceInterfaceState** ](https://msdn.microsoft.com/library/windows/hardware/ff549700)
 [ **IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)
[**KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350) 
[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





