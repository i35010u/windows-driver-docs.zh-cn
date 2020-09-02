---
title: 'WdfSpinlockRelease 规则 (kmdf) '
description: WdfSpinlockRelease 规则指定对 WdfSpinLockAcquire 和 WdfSpinlockRelease 的调用在 KMDF 事件回调函数内按平衡方式使用。
ms.assetid: ecb07a60-d55c-4990-aeef-5c880c13c2a1
ms.date: 05/21/2018
keywords:
- 'WdfSpinlockRelease 规则 (kmdf) '
topic_type:
- apiref
api_name:
- WdfSpinlockRelease
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f77051d3f9855cd002eb3a7f31d0675b9cb3cabe
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381467"
---
# <a name="wdfspinlockrelease-rule-kmdf"></a>WdfSpinLockRelease 规则 (kmdf) 


**WdfSpinLockRelease**规则指定对[**WdfSpinLockAcquire**](/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))和**WdfSpinLockRelease**的调用在 KMDF 事件回调函数内按平衡方式使用。 当 KMDF 事件回调函数返回时，驱动程序不应持有通过先前对 **WdfSpinLockAcquire**的调用获取的框架旋转锁对象。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>WdfSpinLockRelease</strong> 规则。</p>
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
[ **WdfSpinLockRelease**](/previous-versions/windows/hardware/drivers/ff550044(v=vs.85))
 

