---
title: 'SpinLockSafe 规则 (storport) '
description: 此规则验证持有自旋锁时不调用 IoStartNextPacket 和 IoCompleteRequest 例程。
ms.assetid: 12D36178-C00D-44A7-9DA0-E0663DF1FFDC
ms.date: 05/21/2018
keywords:
- 'SpinLockSafe 规则 (storport) '
topic_type:
- apiref
api_name:
- SpinLockSafe
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8a804757100c5a6212497a23cb5a952f257e184f
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382178"
---
# <a name="spinlocksafe-rule-storport"></a>SpinLockSafe 规则 (storport) 


此规则验证持有自旋锁时不调用 **IoStartNextPacket** 和 **IoCompleteRequest** 例程。 此规则跟踪任何时间持有的旋转锁的数量，如果调用其中一个例程，该数字不是0，则驱动程序将无法满足规则。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>SpinLockSafe</strong> 规则。</p>
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

<a name="applies-to"></a>适用于
----------

[**IoAcquireCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff548196(v=vs.85)) 
[**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 
[**IoReleaseCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)) 
[**IoStartNextPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket) 
[**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 
[**KeAcquireSpinLockAtDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel) 
[**KeReleaseSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock) 
[**KeReleaseSpinLockFromDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)
 

