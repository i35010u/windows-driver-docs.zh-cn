---
title: WdfInterruptLockRelease 规则（kmdf）
description: WdfInterruptLockRelease 规则指定对 WdfInterruptAcquireLock 和 WdfInterruptReleaseLock 的调用在 KMDF 回调例程内按平衡方式使用。
ms.assetid: 2cad3811-99c2-4909-bad6-54cab9f006e6
ms.date: 05/21/2018
keywords:
- WdfInterruptLockRelease 规则（kmdf）
topic_type:
- apiref
api_name:
- WdfInterruptLockRelease
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5d4c3e7915a66b1ccd1dd038a4565613225914ac
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917989"
---
# <a name="wdfinterruptlockrelease-rule-kmdf"></a>WdfInterruptLockRelease 规则（kmdf）


**WdfInterruptLockRelease**规则指定对[**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)和[**WdfInterruptReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff547376)的调用在 KMDF 回调例程内按平衡方式使用。 在任何 KMDF 回调例程结束时，驱动程序不应持有通过先前对**WdfInterruptAcquireLock**的调用获取的框架旋转锁对象。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>WdfInterruptLockRelease</strong>规则。</p>
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

[**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340) 
[ **WdfInterruptReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff547376)
 

 





