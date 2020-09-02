---
title: 'CancelSpinLock 规则 (wdm) '
description: CancelSpinLock 规则指定在调用 IoReleaseCancelSpinLock 之前，驱动程序调用 IoAcquireCancelSpinLock，并且驱动程序会在对 IoAcquireCancelSpinLock 的任何后续调用之前调用 IoReleaseCancelSpinLock。
ms.assetid: 8f21a70f-a82b-4b2b-abff-892a1950da41
ms.date: 05/21/2018
keywords:
- 'CancelSpinLock 规则 (wdm) '
topic_type:
- apiref
api_name:
- CancelSpinLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3b94aa3acaa7b14437b3ad548e1cfb9c304f93cf
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382635"
---
# <a name="cancelspinlock-rule-wdm"></a>CancelSpinLock 规则 (wdm) 


CancelSpinLock 规则指定在调用[**IoReleaseCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))之前，驱动程序调用[**IoAcquireCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff548196(v=vs.85)) ，并且驱动程序会在对**IoAcquireCancelSpinLock**的任何后续调用之前调用**IoReleaseCancelSpinLock** 。

此规则还指定在调度例程或取消例程结束时，驱动程序不得保留任何自旋锁。 允许嵌套调用。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>CancelSpinLock</strong> 规则。</p>
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
[**IoReleaseCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)) 
[**RemoveHeadList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-removeheadlist)
 

