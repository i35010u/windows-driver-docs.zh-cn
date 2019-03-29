---
title: StorPortIrql 规则 (storport)
description: StorPortIrql 规则检查，以正确的 IRQL 级别调用 StorPort 例程。
ms.assetid: 6A3946AB-DFB6-4447-9EF3-F0A003DB58E9
ms.date: 05/21/2018
keywords:
- StorPortIrql 规则 (storport)
topic_type:
- apiref
api_name:
- StorPortIrql
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 80d2136af0dd47906761db2370990fa8b51b19a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563424"
---
# <a name="storportirql-rule-storport"></a>StorPortIrql 规则 (storport)


**StorPortIrql**规则检查，以正确的 IRQL 级别调用 StorPort 例程。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>StorPortIrql</strong>规则。</p>
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

[**StorPortAllocateContiguousMemorySpecifyCacheNode**](https://msdn.microsoft.com/library/windows/hardware/ff567027)
[**StorPortAllocateMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff567028) 
 [ **StorPortAllocatePool**](https://msdn.microsoft.com/library/windows/hardware/ff567031)
[**StorPortBuildMdlForNonPagedPool** ](https://msdn.microsoft.com/library/windows/hardware/ff567036) 
 [ **StorPortFreeContiguousMemorySpecifyCache**](https://msdn.microsoft.com/library/windows/hardware/ff567059)
[**StorPortFreeMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff567063) 
 [ **StorPortFreePool**](https://msdn.microsoft.com/library/windows/hardware/ff567065)
[**StorPortGetActiveGroupCount** ](https://msdn.microsoft.com/library/windows/hardware/ff567071) 
 [ **StorPortGetActiveNodeCount**](https://msdn.microsoft.com/library/windows/hardware/ff567073)
[**StorPortGetCurrentProcessorNumber** ](https://msdn.microsoft.com/library/windows/hardware/ff567077) 
 [ **StorPortGetGroupAffinity**](https://msdn.microsoft.com/library/windows/hardware/ff567084)
[**StorPortGetHighestNodeNumber** ](https://msdn.microsoft.com/library/windows/hardware/ff567085) 
 [**StorPortGetLogicalProcessorRelationship**](https://msdn.microsoft.com/library/windows/hardware/ff567087)
[**StorPortGetNodeAffinity** ](https://msdn.microsoft.com/library/windows/hardware/ff567091)
 [ **StorPortGetSystemAddress**](https://msdn.microsoft.com/library/windows/hardware/ff567100)
[**StorPortLogSystemEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff567428) 
 [ **StorPortPutScatterGatherList** ](https://msdn.microsoft.com/library/windows/hardware/ff567463) 
 [ **StorPortRegistryRead**](https://msdn.microsoft.com/library/windows/hardware/ff567491)
[**StorPortRegistryWrite**](https://msdn.microsoft.com/library/windows/hardware/ff567492)
 

 





