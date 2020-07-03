---
title: StorPortStartIo 规则（storport）
description: 永远不能在微型端口的 StartIo 例程中执行等待或数据分配。
ms.assetid: 88CC6D8E-A493-4094-B30B-F6AE67A84B0F
ms.date: 05/21/2018
keywords:
- StorPortStartIo 规则（storport）
topic_type:
- apiref
api_name:
- StorPortStartIo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a1c1a9465e5802c0b65aad201d6cb884b89476f3
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917471"
---
# <a name="storportstartio-rule-storport"></a>StorPortStartIo 规则（storport）


永远不能在微型端口的**StartIo**例程中执行等待或数据分配。 如果该驱动程序调用**StorPortStallExecution**或其他涉及耗时操作的函数，则该驱动程序将无法使用该规则。 由于**StartIo**已同步，因此这些调用通常应在**BuildIo**中完成。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>StorPortStartIo</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**ExAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool) 
[**ExAllocatePoolWithQuota**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquota) 
[**ExAllocatePoolWithQuotaTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag) 
[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 
[**ExAllocatePoolWithTagPriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority) 
[**IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller) 
[**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 
[**IoWMIAllocateInstanceIds**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiallocateinstanceids) 
[**MmAllocateNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory) 
[**MmAllocatePagesForMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdl) 
[**ZwAllocateLocallyUniqueId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-zwallocatelocallyuniqueid) 
[**ZwAllocateVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566416)
 

 





