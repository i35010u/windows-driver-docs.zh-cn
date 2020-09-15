---
title: 'StorPortSpinLock3 规则 (storport) '
description: StorPortSpinLock3 规则验证 StorPortAcquireSpinLock 例程的文档中描述的锁获取层次结构。
ms.assetid: EC637CBD-A45D-44C6-8FAA-7035A36144B6
ms.date: 05/21/2018
keywords:
- 'StorPortSpinLock3 规则 (storport) '
topic_type:
- apiref
api_name:
- StorPortSpinLock3
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0d02b4ca841d223e410b72263d2d0af3108c34d9
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105224"
---
# <a name="storportspinlock3-rule-storport"></a>StorPortSpinLock3 规则 (storport) 


**StorPortSpinLock3**规则验证[**StorPortAcquireSpinLock**](/windows-hardware/drivers/ddi/storport/nf-storport-storportacquirespinlock)例程的文档中描述的锁获取层次结构。

Storport 微型端口驱动程序必须确保它们不会尝试获取已持有的锁或按错误的顺序获取锁。 其中的任何错误都将导致系统死锁。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>StorPortSpinLock3</strong> 规则。</p>
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
