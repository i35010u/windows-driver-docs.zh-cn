---
title: SpinLockSafe 规则（wdm）
description: SpinLockSafe 规则指定在保存旋转锁时不调用 IoStartNextPacket 和 IoCompleteRequest。
ms.assetid: 64a18cb0-80a3-4830-a5b0-131fc1ebdf60
ms.date: 05/21/2018
keywords:
- SpinLockSafe 规则（wdm）
topic_type:
- apiref
api_name:
- SpinLockSafe
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a00c10b74a8b085df8fd93f040542809e5701467
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917811"
---
# <a name="spinlocksafe-rule-wdm"></a>SpinLockSafe 规则（wdm）


**SpinLockSafe**规则指定在保存旋转锁时不调用[**IoStartNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)和[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 。

此规则还指定驱动程序在调用[**KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)或[**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)之前调用[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)或[**KeAcquireSpinLockAtDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel) ，并在调用[**IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))之前调用[**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85)) 。

如果驱动程序包括嵌套的旋转锁，则静态驱动程序验证程序可以报告对该规则的错误冲突，即使已正确获取和释放这些旋转锁。

**驱动程序模型： WDM**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>SpinLockSafe</strong>规则。</p>
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

[**IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85)) 
[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 
[**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)) 
[**IoStartNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket) 
[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 
[**KeAcquireSpinLockRaiseToDpc**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)) 
[**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)
 

 





