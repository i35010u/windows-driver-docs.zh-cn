---
title: 'ReqSendWhileSpinlock 规则 (kmdf) '
description: ReqSendWhileSpinlock 规则指定在驱动程序持有旋转锁时不发送请求。
ms.assetid: f038f4ca-aa24-4df3-9c31-d8eec928c306
ms.date: 05/21/2018
keywords:
- 'ReqSendWhileSpinlock 规则 (kmdf) '
topic_type:
- apiref
api_name:
- ReqSendWhileSpinlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1fdd5e1b7f202c561b197b90c6cec4559cb41dec
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103708"
---
# <a name="reqsendwhilespinlock-rule-kmdf"></a>ReqSendWhileSpinlock 规则 (kmdf) 


**ReqSendWhileSpinlock**规则指定在驱动程序持有旋转锁时不发送请求。

如果驱动程序在包含旋转锁的情况下发送任何请求，则可能会导致死锁或与接收请求的低级驱动程序发生冲突，前提是该驱动程序还尝试获取锁或访问共享资源。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>ReqSendWhileSpinlock</strong> 规则。</p>
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

[**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 
[**WdfSpinLockAcquire**](/previous-versions/windows/hardware/drivers/ff550040(v=vs.85)) 
[**WdfSpinLockRelease**](/previous-versions/windows/hardware/drivers/ff550044(v=vs.85)) 
[**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 
[**KeReleaseSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)另请参阅
--------

[完成 I/o 请求](../wdf/completing-i-o-requests.md) 
[同步取消和完成代码](../wdf/synchronizing-cancel-and-completion-code.md)
