---
title: 'StorPortSpinLock4 规则 (storport) '
description: 此规则是 StorPortSpinLock 的对应发布。 它类似于 SpinLockRelease 规则。
ms.assetid: D6003108-7B97-48A5-9A8B-007DEFB5DF6C
ms.date: 05/21/2018
keywords:
- 'StorPortSpinLock4 规则 (storport) '
topic_type:
- apiref
api_name:
- StorPortSpinLock4
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c61f3771c86b45ccc856e544310ee207b78876ba
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105838"
---
# <a name="storportspinlock4-rule-storport"></a>StorPortSpinLock4 规则 (storport) 


此规则是**StorPortSpinLock**的对应*发布*。 它类似于 **SpinLockRelease** 规则。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>StorPortSpinLock4</strong> 规则。</p>
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

[**StorPortAcquireSpinLock**](/windows-hardware/drivers/ddi/storport/nf-storport-storportacquirespinlock) 
[ **StorPortReleaseSpinLock**](/windows-hardware/drivers/ddi/storport/nf-storport-storportreleasespinlock)
