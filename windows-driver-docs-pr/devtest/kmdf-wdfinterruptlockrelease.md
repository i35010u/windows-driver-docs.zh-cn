---
title: 'WdfInterruptLockRelease 规则 (kmdf) '
description: WdfInterruptLockRelease 规则指定对 WdfInterruptAcquireLock 和 WdfInterruptReleaseLock 的调用在 KMDF 回调例程内按平衡方式使用。
ms.date: 05/21/2018
keywords:
- 'WdfInterruptLockRelease 规则 (kmdf) '
topic_type:
- apiref
api_name:
- WdfInterruptLockRelease
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a7c9a6fadb0a546e515a81dbf1f314cfe7875902
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817441"
---
# <a name="wdfinterruptlockrelease-rule-kmdf"></a>WdfInterruptLockRelease 规则 (kmdf) 


**WdfInterruptLockRelease** 规则指定对 [**WdfInterruptAcquireLock**](/previous-versions/ff547340(v=vs.85))和 [**WdfInterruptReleaseLock**](/previous-versions/ff547376(v=vs.85))的调用在 KMDF 回调例程内按平衡方式使用。 在任何 KMDF 回调例程结束时，驱动程序不应持有通过先前对 **WdfInterruptAcquireLock** 的调用获取的框架旋转锁对象。

**驱动程序模型： KMDF**

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>WdfInterruptLockRelease</strong> 规则。</p>
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

[**WdfInterruptAcquireLock**](/previous-versions/ff547340(v=vs.85)) 
[ **WdfInterruptReleaseLock**](/previous-versions/ff547376(v=vs.85))
