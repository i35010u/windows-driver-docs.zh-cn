---
title: SpNoWait 规则 (storport)
description: 此规则验证等待或数据分配不会在 StartIo 内执行。
ms.assetid: 4E1FABD1-AA6B-4EA1-BDD8-0C7A46AFF19B
ms.date: 05/21/2018
keywords:
- SpNoWait 规则 (storport)
topic_type:
- apiref
api_name:
- SpNoWait
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0dd838cb02c1d7d7630de1afef452e6848fc8454
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345691"
---
# <a name="spnowait-rule-storport"></a>SpNoWait 规则 (storport)


此规则验证等待或数据分配不会执行内部**StartIo**。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>SpNoWait</strong>规则。</p>
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

[**StorPortStallExecution**](https://msdn.microsoft.com/library/windows/hardware/ff567508)
[**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)
[**ExAllocatePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544501) 
 [ **ExAllocatePoolWithQuota**](https://msdn.microsoft.com/library/windows/hardware/ff544506)
[**ExAllocatePoolWithQuotaTag**](https://msdn.microsoft.com/library/windows/hardware/ff544513) 
 [ **ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520)
[**ExAllocatePoolWithTagPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff544523)
 [ **ExWaitForRundownProtectionRelease**](https://msdn.microsoft.com/library/windows/hardware/jj569378)
[**IoAllocateController** ](https://msdn.microsoft.com/library/windows/hardware/ff548224)
 [ **IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)
[**IoWMIAllocateInstanceIds** ](https://msdn.microsoft.com/library/windows/hardware/ff550429) 
[ **KeWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff553324)
[**KeWaitForMutexObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553344)
 [ **KeWaitForSingleObject**](https://msdn.microsoft.com/library/windows/hardware/ff553350)
[**MmAllocateNonCachedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff554479) 
 [ **MmAllocatePagesForMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff554482) 
 [ **ZwAllocateLocallyUniqueId**](https://msdn.microsoft.com/library/windows/hardware/ff566415)
[**ZwAllocateVirtualMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff566416) 
 [ **ZwWaitForSingleObject**](https://msdn.microsoft.com/library/windows/hardware/ff567120)
 

 





