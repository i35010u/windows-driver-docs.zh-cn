---
title: 'StorPortSpinLock 规则 (storport) '
description: 此规则验证通过 StorPortReleaseSpinLock 获取的锁定是否立即通过发布。
ms.assetid: B7B918A0-3042-4961-8D33-EFDC15819D1F
ms.date: 05/21/2018
keywords:
- 'StorPortSpinLock 规则 (storport) '
topic_type:
- apiref
api_name:
- StorPortSpinLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 210196a0bcb99724d3aaeadd482d7b45644c1abb
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384093"
---
# <a name="storportspinlock-rule-storport"></a>StorPortSpinLock 规则 (storport) 


此规则验证通过 StorPortReleaseSpinLock 获取的**锁定是否立即通过** **StorPortReleaseSpinLock**发布。 如果小型小型驱动程序尝试获取已获取的锁定，或者尝试释放尚未获取的锁定，则该规则将无法使用该规则。 此外，在调度或取消例程结束时，驱动程序不应持有任何自旋锁。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>StorPortSpinLock</strong> 规则。</p>
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

[**StorPortAcquireSpinLock**](/windows-hardware/drivers/ddi/storport/nf-storport-storportacquirespinlock) 
[ **StorPortReleaseSpinLock**](/windows-hardware/drivers/ddi/storport/nf-storport-storportreleasespinlock)
 

