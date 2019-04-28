---
title: IrqlDispatch 规则 (storport)
description: 此规则验证以下例程仅调用在 IRQL 调度\_级别。
ms.assetid: 93ABD54D-4D63-495A-917B-A387C9353969
ms.date: 05/21/2018
keywords:
- IrqlDispatch 规则 (storport)
topic_type:
- apiref
api_name:
- IrqlDispatch
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 008fa6c1fe3dfc6c7398bd563a1f7331d48dcef6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345745"
---
# <a name="irqldispatch-rule-storport"></a>IrqlDispatch 规则 (storport)


此规则验证，仅在调用以下例程**IRQL = 调度\_级别**。

-   AllocateAdapterChannel

-   FreeAdapterChannel

-   FreeMapRegisters

-   GetScatterGatherList

-   IoAllocateController

-   IoFreeController

-   IoStartNextPacket

-   KeAcquireSpinLockAtDpcLevel

-   KeInsertByKeyDeviceQueue

-   KeInsertDeviceQueue

-   KeReleaseSpinLockFromDpcLevel

-   KeRemoveByKeyDeviceQueue

-   KeRemoveDeviceQueue

-   PutScatterGatherList

|              |          |
|--------------|----------|
| 驱动程序模型 | Storport |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrqlDispatch</strong>规则。</p>
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

[**AllocateAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff540573)
[**FreeAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff546507)
[**FreeMapRegisters** ](https://msdn.microsoft.com/library/windows/hardware/ff546513) 
 [ **GetScatterGatherList**](https://msdn.microsoft.com/library/windows/hardware/ff546531)
[**IoAllocateController** ](https://msdn.microsoft.com/library/windows/hardware/ff548224)
 [ **IoFreeController**](https://msdn.microsoft.com/library/windows/hardware/ff549104)
[**IoStartNextPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550358) 
 [**KeAcquireSpinLockAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff551921)
[**KeInsertByKeyDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff552178) 
 [**KeInsertDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff552180)
[**KeReleaseSpinLockFromDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff553150) 
 [ **KeRemoveByKeyDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff553152)
[**KeRemoveDeviceQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff553156) 
 [ **PutScatterGatherList**](https://msdn.microsoft.com/library/windows/hardware/ff559967)
 

 





