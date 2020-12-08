---
title: 'StorPortIrql 规则 (storport) '
description: StorPortIrql 规则检查 StorPort 例程是否是以正确的 IRQL 级别调用的。
ms.date: 05/21/2018
keywords:
- 'StorPortIrql 规则 (storport) '
topic_type:
- apiref
api_name:
- StorPortIrql
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d9f9ec64e058e101b4ff1e6e7c9d247b8867bad6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822555"
---
# <a name="storportirql-rule-storport"></a>StorPortIrql 规则 (storport) 


**StorPortIrql** 规则检查 StorPort 例程是否是以正确的 IRQL 级别调用的。

**驱动程序模型： Storport**

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>StorPortIrql</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**StorPortAllocateContiguousMemorySpecifyCacheNode**](/windows-hardware/drivers/ddi/storport/nf-storport-storportallocatecontiguousmemoryspecifycachenode) 
[**StorPortAllocateMdl**](/windows-hardware/drivers/ddi/storport/nf-storport-storportallocatemdl) 
[**StorPortAllocatePool**](/windows-hardware/drivers/ddi/storport/nf-storport-storportallocatepool) 
[**StorPortBuildMdlForNonPagedPool**](/windows-hardware/drivers/ddi/storport/nf-storport-storportbuildmdlfornonpagedpool) 
[**StorPortFreeContiguousMemorySpecifyCache**](/windows-hardware/drivers/ddi/storport/nf-storport-storportfreecontiguousmemoryspecifycache) 
[**StorPortFreeMdl**](/windows-hardware/drivers/ddi/storport/nf-storport-storportfreemdl) 
[**StorPortFreePool**](/windows-hardware/drivers/ddi/storport/nf-storport-storportfreepool) 
[**StorPortGetActiveGroupCount**](/windows-hardware/drivers/ddi/storport/nf-storport-storportgetactivegroupcount) 
[**StorPortGetActiveNodeCount**](/windows-hardware/drivers/ddi/storport/nf-storport-storportgetactivenodecount) 
[**StorPortGetCurrentProcessorNumber**](/windows-hardware/drivers/ddi/storport/nf-storport-storportgetcurrentprocessornumber) 
[**StorPortGetGroupAffinity**](/windows-hardware/drivers/ddi/storport/nf-storport-storportgetgroupaffinity) 
[**StorPortGetHighestNodeNumber**](/windows-hardware/drivers/ddi/storport/nf-storport-storportgethighestnodenumber) 
[**StorPortGetLogicalProcessorRelationship**](/windows-hardware/drivers/ddi/storport/nf-storport-storportgetlogicalprocessorrelationship) 
[**StorPortGetNodeAffinity**](/windows-hardware/drivers/ddi/storport/nf-storport-storportgetnodeaffinity) 
[**StorPortGetSystemAddress**](/windows-hardware/drivers/ddi/storport/nf-storport-storportgetsystemaddress) 
[**StorPortLogSystemEvent**](/windows-hardware/drivers/ddi/storport/nf-storport-storportlogsystemevent) 
[**StorPortPutScatterGatherList**](/windows-hardware/drivers/ddi/storport/nf-storport-storportputscattergatherlist) 
[**StorPortRegistryRead**](/windows-hardware/drivers/ddi/storport/nf-storport-storportregistryread) 
[**StorPortRegistryWrite**](/windows-hardware/drivers/ddi/storport/nf-storport-storportregistrywrite)
