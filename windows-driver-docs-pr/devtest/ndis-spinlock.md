---
title: '旋转锁规则 (ndis) '
description: 旋转锁规则验证 NDIS 旋转锁定接口的正确使用。
ms.assetid: 27A20B0C-A1B9-40E6-BA9D-64BB9F58B027
ms.date: 05/21/2018
keywords:
- '旋转锁规则 (ndis) '
topic_type:
- apiref
api_name:
- SpinLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2802c202239900d90b4eb7e7ab0a23ac51a96072
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102214"
---
# <a name="spinlock-rule-ndis"></a>旋转锁规则 (ndis) 


**旋转锁**规则验证 NDIS 旋转锁定接口的正确使用。 此规则指定仅当旋转锁处于解锁状态时才对 [**NdisAcquireSpinLock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirespinlock) 进行调用。 此规则还将验证旋转锁是否在微型端口处理程序例程退出之前被释放。

**驱动程序模型： NDIS**

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>旋转锁</strong> 规则。</p>
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

[**NdisAcquireSpinLock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirespinlock) 
[**NdisDprAcquireSpinLock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdpracquirespinlock) 
[**NdisDprReleaseSpinLock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdprreleasespinlock) 
[**NdisReleaseSpinLock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreleasespinlock)
