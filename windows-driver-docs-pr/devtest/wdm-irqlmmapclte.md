---
title: IrqlMmApcLte 规则（wdm）
ms.assetid: 075f5710-b2bf-4546-9648-661a3c8521f8
ms.date: 05/21/2018
description: ''
keywords:
- IrqlMmApcLte 规则（wdm）
topic_type:
- apiref
api_name:
- IrqlMmApcLte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4d35c02186b7a2e796fe7402be7d0b188946df75
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917269"
---
# <a name="irqlmmapclte-rule-wdm"></a>IrqlMmApcLte 规则（wdm）


**IrqlMmApcLte**规则指定仅当驱动程序在 IRQL &lt; = APC 级别执行时才调用以下内存管理器例程 \_ ：

-   [**MmAllocateNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory)

-   [**MmFreeNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmfreenoncachedmemory)

-   [**MmAllocatePagesForMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdl)

-   [**MmFreePagesFromMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreepagesfrommdl)

-   [**MmLockPagableDataSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagabledatasection)

-   [**MmLockPagableSectionByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmlockpagablesectionbyhandle)

-   [**MmPageEntireDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmpageentiredriver)

-   [**MmResetDriverPaging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmresetdriverpaging)

-   [**MmSecureVirtualMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmsecurevirtualmemory)

-   [**MmUnlockPagableImageSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpagableimagesection)

-   [**MmUnsecureVirtualMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmunsecurevirtualmemory)

**驱动程序模型： WDM**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 找到了具有此规则的 Bug 检查 | [**Bug 检查0xC4：驱动程序 \_\_检测到 \_ 验证程序冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x00020019） |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>IrqlMmApcLte</strong>规则。</p>
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

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">驱动程序验证程序</a>，并选择 " <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 相容性检查</a>" 选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**MmAllocateNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory) 
[**MmAllocatePagesForMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdl) 
[**MmAllocatePagesForMdlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdlex) 
[**MmFreeNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmfreenoncachedmemory) 
[**MmFreePagesFromMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreepagesfrommdl) 
[**MmLockPagableDataSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagabledatasection) 
[**MmLockPagableSectionByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmlockpagablesectionbyhandle) 
[**MmPageEntireDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmpageentiredriver) 
[**MmResetDriverPaging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmresetdriverpaging) 
[**MmSecureVirtualMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmsecurevirtualmemory) 
[**MmUnlockPagableImageSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpagableimagesection) 
[**MmUnsecureVirtualMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmunsecurevirtualmemory)
 

 





