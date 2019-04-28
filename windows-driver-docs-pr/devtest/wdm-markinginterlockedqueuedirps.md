---
title: MarkingInterlockedQueuedIrps 规则 (wdm)
description: MarkingInterlockedQueuedIrps 规则指定的驱动程序正确地将 IRP 标记为挂起之前它对其进行排队以进行进一步处理互锁的方式。
ms.assetid: a065b28f-f02a-45af-b9d9-754a36519b99
ms.date: 05/21/2018
keywords:
- MarkingInterlockedQueuedIrps 规则 (wdm)
topic_type:
- apiref
api_name:
- MarkingInterlockedQueuedIrps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 35eb90dcf17ab43520e159d61b524829772a380c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331346"
---
# <a name="markinginterlockedqueuedirps-rule-wdm"></a>MarkingInterlockedQueuedIrps 规则 (wdm)


**MarkingInterlockedQueuedIrps**规则指定的驱动程序正确将 IRP 标记为挂起之前它对其进行排队以进行进一步的处理方式互锁。

此规则还指定驱动程序调用[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)并正确地将 IRP 标记为挂起的之前调用任意以下函数以将 IRP 添加到互锁队列：

-   [**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397)

-   [**ExInterlockedInsertTailList**](https://msdn.microsoft.com/library/windows/hardware/ff545402)

-   [**ExInterlockedPushEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545418)

驱动程序应调用[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)然后再添加需要到互锁队列的更多处理 IRP。 否则为无法取消排队，另一个驱动程序例程，完成并释放通过对调用之前系统 IRP **IoMarkIrpPending**发生，从而会导致崩溃。

有关详细信息，请参阅[**同步 IRP 取消**](https://msdn.microsoft.com/library/windows/hardware/ff564531)。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>MarkingInterlockedQueuedIrps</strong>规则。</p>
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

[**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397)
[**ExInterlockedInsertTailList** ](https://msdn.microsoft.com/library/windows/hardware/ff545402) 
 [ **ExInterlockedPushEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545418)
[**IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422) 
 [ **RemoveHeadList** ](https://msdn.microsoft.com/library/windows/hardware/ff561032)另请参阅
--------

[**MarkIrpPending**](wdm-markirppending.md)
[**同步 IRP 取消**](https://msdn.microsoft.com/library/windows/hardware/ff564531)
 

 





