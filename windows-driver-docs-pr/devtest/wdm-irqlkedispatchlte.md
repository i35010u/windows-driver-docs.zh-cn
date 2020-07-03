---
title: IrqlKeDispatchLte 规则（wdm）
ms.assetid: 425a20ea-c9e3-45f4-a517-6bad9ab0de98
ms.date: 05/21/2018
description: ''
keywords:
- IrqlKeDispatchLte 规则（wdm）
topic_type:
- apiref
api_name:
- IrqlKeDispatchLte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 368a927303267dff6ae6fa1e8260f2049c9980fb
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917909"
---
# <a name="irqlkedispatchlte-rule-wdm"></a>IrqlKeDispatchLte 规则（wdm）


**IrqlKeDispatchLte**规则指定仅当驱动程序在 IRQL &lt; = 调度级别执行时才调用以下内核例程 \_ ：

-   [**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)

-   [**KeCancelTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kecanceltimer)

-   [**KeClearEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keclearevent)

-   [**KeFlushIoBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers)

-   [**KeInitializeDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedevicequeue)

-   [**KeInitializeTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimer)

-   [**KeInitializeTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimerex)

-   [**KePulseEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kepulseevent)

-   [**KeRaiseIrqlToDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)

-   [**KeReadStateEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereadstateevent)

-   [**KeReadStateTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereadstatetimer)

-   [**KeReleaseMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex)

-   [**KeRemoveEntryDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremoveentrydevicequeue)

-   [**KeResetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keresetevent)

-   [**KeSaveFloatingPointState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesavefloatingpointstate)

-   [**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer)

-   [**KeSetTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex)

**驱动程序模型： WDM**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 找到了具有此规则的 Bug 检查 | [**Bug 检查0xC4：驱动程序 \_\_检测到 \_ 验证程序冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x00020011） |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>IrqlKeDispatchLte</strong>规则。</p>
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

[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 
[**KeCancelTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kecanceltimer) 
[**KeClearEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keclearevent) 
[**KeInitializeDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedevicequeue) 
[**KeInitializeSemaphore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializesemaphore) 
[**KeInitializeTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimer) 
[**KeInitializeTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializetimerex) 
[**KePulseEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kepulseevent) 
[**KeReadStateEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereadstateevent) 
[**KeReadStateTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereadstatetimer) 
[**KeReleaseMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex) 
[**KeRemoveEntryDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremoveentrydevicequeue) 
[**KeResetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keresetevent) 
[**KeSaveFloatingPointState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesavefloatingpointstate) 
[**KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer) 
[**KeSetTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex)
 

 





