---
title: 'WdfSpinlock 规则 (kmdf) '
description: WdfSpinlock 规则指定对 WdfSpinLockAcquire 方法的调用与 WdfSpinlockRelease 一起用于严格替换。
ms.assetid: bf95509a-29f7-462d-b883-39aca4193ebb
ms.date: 05/21/2018
keywords:
- 'WdfSpinlock 规则 (kmdf) '
topic_type:
- apiref
api_name:
- WdfSpinlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fb4e2b40ab398000c4233530d8cfd89fdea2e232
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381505"
---
# <a name="wdfspinlock-rule-kmdf"></a>WdfSpinlock 规则 (kmdf) 


**WdfSpinlock**规则指定对[**WdfSpinLockAcquire**](/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))方法的调用与[**WdfSpinlockRelease**](kmdf-wdfspinlockrelease.md)一起用于严格替换。 在任何 KMDF 回调例程结束时，驱动程序不应持有先前对 **WdfSpinLockAcquire**的调用获取的框架旋转锁对象。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>WdfSpinlock</strong> 规则。</p>
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

[**WdfSpinLockAcquire**](/previous-versions/windows/hardware/drivers/ff550040(v=vs.85)) 
[**WdfSpinLockCreate**](/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfspinlockcreate) 
[**WdfSpinLockRelease**](/previous-versions/windows/hardware/drivers/ff550044(v=vs.85))
 

