---
title: ChangeQueueState 规则 (kmdf)
description: ChangeQueueState 规则指定 WDF 驱动程序不会尝试从并发线程更改队列的状态或不会调用更改 DDIs 一个接一个从同一线程内的状态。
ms.assetid: C05A04E8-F8F2-4339-AAB7-FD62BE1DAAA2
ms.date: 05/21/2018
keywords:
- ChangeQueueState 规则 (kmdf)
topic_type:
- apiref
api_name:
- ChangeQueueState
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e9f1bc407c192dbb431fa9d229405c1c88f7edaa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542362"
---
# <a name="changequeuestate-rule-kmdf"></a>ChangeQueueState 规则 (kmdf)


**ChangeQueueState**规则指定 WDF 驱动程序不会尝试从并发线程更改队列的状态或不会调用更改 DDIs 一个接一个从同一线程内的状态。 队列的状态不断变化的回调函数非常[ **WdfIoQueueStop**](https://msdn.microsoft.com/library/windows/hardware/ff548482)， [ **WdfIoQueueStopSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548489)，[ **WdfIoQueuePurge**](https://msdn.microsoft.com/library/windows/hardware/ff548442)，[**WdfIoQueuePurgeSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548449)， [ **WdfIoQueueDrain** ](https://msdn.microsoft.com/library/windows/hardware/ff547406)， [ **WdfIoQueueDrainSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff547412)， [ **WdfIoQueueStopAndPurge** ](https://msdn.microsoft.com/library/windows/hardware/hh439289)和[ **WdfIoQueueStopAndPurgeSynchronously**](https://msdn.microsoft.com/library/windows/hardware/hh439293)。 如果正在处理队列状态更改时调用这些 DDIs 它将导致计算机崩溃或停止响应。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>ChangeQueueState</strong>规则。</p>
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

[**WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)
[**WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)
[**WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)
 [ **WdfIoQueueDrain**](https://msdn.microsoft.com/library/windows/hardware/ff547406)
[**WdfIoQueueDrainSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff547412) 
 [ **WdfIoQueuePurge**](https://msdn.microsoft.com/library/windows/hardware/ff548442)
[**WdfIoQueuePurgeSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548449) 
 [**WdfIoQueueStop**](https://msdn.microsoft.com/library/windows/hardware/ff548482)
[**WdfIoQueueStopAndPurge** ](https://msdn.microsoft.com/library/windows/hardware/hh439289) 
 [ **WdfIoQueueStopAndPurgeSynchronously**](https://msdn.microsoft.com/library/windows/hardware/hh439293)
[**WdfIoQueueStopSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548489)
 

 





