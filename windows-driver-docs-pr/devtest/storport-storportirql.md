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
ms.openlocfilehash: dc0eb437e406493cd6240481c2125a9c8c208940
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391844"
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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>StorPortIrql</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**StorPortAllocateContiguousMemorySpecifyCacheNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportallocatecontiguousmemoryspecifycachenode)
[**StorPortAllocateMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportallocatemdl) 
 [ **StorPortAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportallocatepool)
[**StorPortBuildMdlForNonPagedPool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportbuildmdlfornonpagedpool) 
 [ **StorPortFreeContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportfreecontiguousmemoryspecifycache)
[**StorPortFreeMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportfreemdl) 
 [ **StorPortFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportfreepool)
[**StorPortGetActiveGroupCount** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetactivegroupcount) 
 [ **StorPortGetActiveNodeCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetactivenodecount)
[**StorPortGetCurrentProcessorNumber** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetcurrentprocessornumber) 
 [ **StorPortGetGroupAffinity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetgroupaffinity)
[**StorPortGetHighestNodeNumber** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgethighestnodenumber) 
 [**StorPortGetLogicalProcessorRelationship**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetlogicalprocessorrelationship)
[**StorPortGetNodeAffinity** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetnodeaffinity)
 [ **StorPortGetSystemAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetsystemaddress)
[**StorPortLogSystemEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportlogsystemevent) 
 [ **StorPortPutScatterGatherList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportputscattergatherlist) 
 [ **StorPortRegistryRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportregistryread)
[**StorPortRegistryWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportregistrywrite)
 

 





