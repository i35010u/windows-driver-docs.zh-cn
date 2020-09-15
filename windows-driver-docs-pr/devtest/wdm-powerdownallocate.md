---
title: 'PowerDownAllocate 规则 (wdm) '
description: PowerDownAllocate 规则指定 FDO 和 FIDO 驱动程序在处理 IRP \_ MN \_ \_ 为从 S0 到 \ S1 的 SystemPowerState 转换处理 IRP 设置电源请求时不应分配内存 .。。S5 \。
ms.assetid: 01737B5F-C1DF-4012-85F2-E9B7517EA53A
ms.date: 05/21/2018
keywords:
- 'PowerDownAllocate 规则 (wdm) '
topic_type:
- apiref
api_name:
- PowerDownAllocate
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a84b94f084ad21bad6fa2d9a81848a812d73560b
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102783"
---
# <a name="powerdownallocate-rule-wdm"></a>PowerDownAllocate 规则 (wdm) 


**PowerDownAllocate**规则指定 FDO 和 FIDO 驱动程序在处理 IRP \_ MN \_ \_ 为从 s0 到 S1 的**SystemPowerState**转换处理 IRP 设置电源请求时不应分配内存 \[ .。。S5 \] 。

此规则仅适用于 FDO 和 FIDO 驱动程序。

**驱动程序模型： WDM**

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>PowerDownAllocate</strong> 规则。</p>
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

[**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 
[ **IoAcquireRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)
