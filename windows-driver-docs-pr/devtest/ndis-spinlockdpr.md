---
title: SpinLockDpr 规则 (ndis)
description: SpinLockDpr 规则验证 NDIS 数值调节钮锁定接口的正确用法。此规则指定仅当自旋锁处于解锁状态时进行调用 NdisDprAcquireSpinLock。
ms.assetid: 60056fae-54d1-4365-bcb5-02c63e4fb521
ms.date: 05/21/2018
keywords:
- SpinLockDpr 规则 (ndis)
topic_type:
- apiref
api_name:
- SpinLockDpr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5356e8b3852f5f3a8f5ecdf773c6571a5ac5bb43
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392169"
---
# <a name="spinlockdpr-rule-ndis"></a>SpinLockDpr 规则 (ndis)


**SpinLockDpr**规则验证 NDIS 数值调节钮锁定接口的正确用法。

此规则指定的调用[ **NdisDprAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisdpracquirespinlock)只有自旋锁处于解锁状态时进行。 此规则还会验证微型端口处理程序例程退出之前释放自旋锁。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>SpinLockDpr</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**NdisAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisacquirespinlock)
[**NdisAllocateSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatespinlock)
[**NdisDprAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisdpracquirespinlock)
[**NdisDprReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisdprreleasespinlock)
[**NdisReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreleasespinlock)
 

 





