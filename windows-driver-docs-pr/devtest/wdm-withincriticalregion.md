---
title: WithinCriticalRegion 规则 (wdm)
description: WithinCriticalRegion 规则指定对特定同步函数的驱动程序的调用出现仅之后调用 KeEnterCriticalRegion 和之前调用 KeLeaveCriticalRegion。
ms.assetid: 9b74b868-6025-4e81-b5ba-21e0da734cd9
ms.date: 05/21/2018
keywords:
- WithinCriticalRegion 规则 (wdm)
topic_type:
- apiref
api_name:
- WithinCriticalRegion
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3f617c567bb42c01440a5d643bf229dbd709c939
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526233"
---
# <a name="withincriticalregion-rule-wdm"></a>WithinCriticalRegion 规则 (wdm)


**WithinCriticalRegion**规则指定对特定同步函数的驱动程序的调用出现在调用后才[ **KeEnterCriticalRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552021)和然后再调用[ **KeLeaveCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552964)。

受影响的同步函数如下所示：

-   [**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)

-   [**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)

-   [**ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)

-   [**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)

-   [**ExReleaseResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545597)

-   [**ExReleaseResourceForThreadLite**](https://msdn.microsoft.com/library/windows/hardware/ff545585)

此规则不识别禁用正常 APC 交付的其他方法。 有关详细信息，请参阅[**禁用 Apc**](https://msdn.microsoft.com/library/windows/hardware/ff543219)。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>WithinCriticalRegion</strong>规则。</p>
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

[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)
[**ExAcquireResourceSharedLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544363) 
 [ **ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)
[**ExAcquireSharedWaitForExclusive** ](https://msdn.microsoft.com/library/windows/hardware/ff544370) 
 [ **ExReleaseResourceForThreadLite**](https://msdn.microsoft.com/library/windows/hardware/ff545585)
[**ExReleaseResourceLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545597) 
 [ **KeEnterCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552021)
[**KeEnterGuardedRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552028) 
 [ **KeLeaveCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552964)
[**KeLeaveGuardedRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552967)另请参阅
--------

[**管理硬件优先级**](https://msdn.microsoft.com/library/windows/hardware/ff554368)
[**使用自旋锁的同时防止错误和死锁**](https://msdn.microsoft.com/library/windows/hardware/ff559854)
 

 





