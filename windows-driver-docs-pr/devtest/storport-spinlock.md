---
title: 旋转锁规则（storport）
description: 此规则验证是否立即调用 KeAcquireSpinLock，然后调用 KeReleaseSpinlock。
ms.assetid: 7D06327F-CE74-4337-8B5C-79189FE15F2F
ms.date: 05/21/2018
keywords:
- 旋转锁规则（storport）
topic_type:
- apiref
api_name:
- SpinLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c489b740fcdf44548dbe53dc8486d7fa5e181751
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916712"
---
# <a name="spinlock-rule-storport"></a>旋转锁规则（storport）


此规则验证是否立即调用**KeAcquireSpinLock** ，然后调用**KeReleaseSpinlock**。 如果驱动程序在释放锁之前再次调用**KeAcquireSpinLockRaiseToDpc**或**KeAcquireSpinLock** ，则该规则将失败。 此外，在退出调度或取消例程之前，驱动程序必须释放旋转锁。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>旋转锁</strong>规则。</p>
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

[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 
[**KeAcquireSpinLockRaiseToDpc**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)) 
[**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)
 

 





