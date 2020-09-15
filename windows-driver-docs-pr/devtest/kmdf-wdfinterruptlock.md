---
title: 'WdfInterruptLock 规则 (kmdf) '
description: WdfInterruptLock 规则指定对 WdfInterruptAcquireLock 方法的调用在严格替换中用于对 WdfInterruptReleaseLock 的调用。
ms.assetid: bf105e83-dc63-44b1-ba9d-e4d81210fa1a
ms.date: 05/21/2018
keywords:
- 'WdfInterruptLock 规则 (kmdf) '
topic_type:
- apiref
api_name:
- WdfInterruptLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3ad7a1711a8bdf0a2861f6e9e1ce518e9a4d7393
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105046"
---
# <a name="wdfinterruptlock-rule-kmdf"></a>WdfInterruptLock 规则 (kmdf) 


**WdfInterruptLock**规则指定对[**WdfInterruptAcquireLock**](/previous-versions/ff547340(v=vs.85))方法的调用在严格替换中用于对[**WdfInterruptReleaseLock**](/previous-versions/ff547376(v=vs.85))的调用。 此外，在任何 KMDF 回调例程结束时，驱动程序不应持有框架旋转锁对象，这是由先前对 **WdfInterruptAcquireLock**的调用获得的。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>WdfInterruptLock</strong> 规则。</p>
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
