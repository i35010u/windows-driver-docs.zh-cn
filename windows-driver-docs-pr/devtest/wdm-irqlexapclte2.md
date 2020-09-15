---
title: 'IrqlExApcLte2 规则 (wdm) '
description: IrqlExApcLte2 规则指定驱动程序仅在 IRQL APC 级别调用以下例程 \_ 。
ms.assetid: 5800ec58-2084-4092-9614-dd631458c7dd
ms.date: 05/21/2018
keywords:
- 'IrqlExApcLte2 规则 (wdm) '
topic_type:
- apiref
api_name:
- IrqlExApcLte2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b891c787ddb8bac88b39e0b904b86fc5fc4fb0f2
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105564"
---
# <a name="irqlexapclte2-rule-wdm"></a>IrqlExApcLte2 规则 (wdm) 


**IrqlExApcLte2**规则指定该驱动程序仅在 IRQL &lt; = APC 级别调用以下例程 \_ 。

-   [**CmRegisterCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallback)

-   [**CmUnRegisterCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-cmunregistercallback)

-   [**ExAllocateFromPagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatefrompagedlookasidelist)

-   [**ExAllocatePoolWithQuota**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquota)

-   [**ExAllocatePoolWithQuotaTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag)

-   [**ExDeletePagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletepagedlookasidelist)

-   [**ExFreeToPagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetopagedlookasidelist)

-   [**ExInitializePagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepagedlookasidelist)

-   [**ExRegisterCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exregistercallback)

-   [**ExSetTimerResolution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimerresolution)

-   [**ExUnregisterCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exunregistercallback)

-   [**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)

-   [**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)

**驱动程序模型： WDM**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0X00020006) ， [**bug 检查0xA： IRQL \_ 不 \_ 小于 \_ 或 \_ 等于**](../debugger/bug-check-0xa--irql-not-less-or-equal.md)


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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IrqlExApcLte2</strong> 规则。</p>
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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 " <a href="/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](./ddi-compliance-checking.md)">DDI 相容性检查</a> " 选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**CmRegisterCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallback) 
[**CmRegisterCallbackEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex) 
[**CmUnRegisterCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-cmunregistercallback) 
[**ExDeletePagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletepagedlookasidelist) 
[**ExInitializePagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepagedlookasidelist) 
[**ExRegisterCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exregistercallback) 
[**ExSetTimerResolution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimerresolution) 
[**ExUnregisterCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exunregistercallback) 
[**ProbeForRead**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread) 
[**ProbeForWrite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)
