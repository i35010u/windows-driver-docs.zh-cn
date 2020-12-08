---
title: 'IrqlKeDispatchLte 规则 (wdm) '
ms.date: 05/21/2018
description: '了解详细信息： IrqlKeDispatchLte 规则 (wdm) '
keywords:
- 'IrqlKeDispatchLte 规则 (wdm) '
topic_type:
- apiref
api_name:
- IrqlKeDispatchLte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 56901dd2b43b35e9d3d986700cb9a2ed04121b03
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791845"
---
# <a name="irqlkedispatchlte-rule-wdm"></a>IrqlKeDispatchLte 规则 (wdm) 


**IrqlKeDispatchLte** 规则指定仅当驱动程序在 IRQL &lt; = 调度级别执行时才调用以下内核例程 \_ ：

-   [**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)

-   [**KeCancelTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kecanceltimer)

-   [**KeClearEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keclearevent)

-   [**KeFlushIoBuffers**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers)

-   [**KeInitializeDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedevicequeue)

-   [**KeInitializeTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimer)

-   [**KeInitializeTimerEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimerex)

-   [**KePulseEvent**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kepulseevent)

-   [**KeRaiseIrqlToDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)

-   [**KeReadStateEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereadstateevent)

-   [**KeReadStateTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereadstatetimer)

-   [**KeReleaseMutex**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)

-   [**KeRemoveEntryDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keremoveentrydevicequeue)

-   [**KeResetEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keresetevent)

-   [**KeSaveFloatingPointState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesavefloatingpointstate)

-   [**KeSetTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer)

-   [**KeSetTimerEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex)

**驱动程序模型： WDM**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00020011) 


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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IrqlKeDispatchLte</strong> 规则。</p>
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

[**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 
[**KeCancelTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kecanceltimer) 
[**KeClearEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keclearevent) 
[**KeInitializeDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedevicequeue) 
[**KeInitializeSemaphore**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializesemaphore) 
[**KeInitializeTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimer) 
[**KeInitializeTimerEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimerex) 
[**KePulseEvent**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kepulseevent) 
[**KeReadStateEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereadstateevent) 
[**KeReadStateTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereadstatetimer) 
[**KeReleaseMutex**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex) 
[**KeRemoveEntryDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keremoveentrydevicequeue) 
[**KeResetEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keresetevent) 
[**KeSaveFloatingPointState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesavefloatingpointstate) 
[**KeSetTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer) 
[**KeSetTimerEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex)
