---
title: 'IrqlKeApcLte1 规则 (wdm) '
ms.assetid: d88e3c0f-574b-41df-97ee-282a9f1eb6f4
ms.date: 05/21/2018
description: ''
keywords:
- 'IrqlKeApcLte1 规则 (wdm) '
topic_type:
- apiref
api_name:
- IrqlKeApcLte1
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ba086a95ecc9a39bb8a07920d6a37bd0b5a40052
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384479"
---
# <a name="irqlkeapclte1-rule-wdm"></a>IrqlKeApcLte1 规则 (wdm) 


**IrqlKeApcLte1**规则指定仅当驱动程序在 IRQL &lt; = APC 级别执行时才调用以下内核例程 \_ ：

-   [**KeAcquireGuardedMutex**](/previous-versions/windows/hardware/drivers/ff551892(v=vs.85))

-   [**KeAcquireGuardedMutexUnsafe**](/previous-versions/windows/hardware/drivers/ff551894(v=vs.85))

-   [**KeDelayExecutionThread**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kedelayexecutionthread)

-   [**KeQueryActiveProcessors**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kequeryactiveprocessors)

-   [**KeReleaseGuardedMutex**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseguardedmutex)

-   [**KeReleaseGuardedMutexUnsafe**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseguardedmutexunsafe)

-   [**KeTryToAcquireGuardedMutex**](/previous-versions/ff553307(v=vs.85))

**驱动程序模型： WDM**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x0002000F) 


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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IrqlKeApcLte1</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 " <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](./ddi-compliance-checking.md)">DDI 相容性检查</a> " 选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**KeAcquireGuardedMutex**](/previous-versions/windows/hardware/drivers/ff551892(v=vs.85)) 
[**KeAcquireGuardedMutexUnsafe**](/previous-versions/windows/hardware/drivers/ff551894(v=vs.85)) 
[**KeDelayExecutionThread**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kedelayexecutionthread) 
[**KeQueryActiveProcessors**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kequeryactiveprocessors) 
[**KeReleaseGuardedMutex**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseguardedmutex) 
[**KeReleaseGuardedMutexUnsafe**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseguardedmutexunsafe) 
[**KeTryToAcquireGuardedMutex**](/previous-versions/ff553307(v=vs.85))
 

