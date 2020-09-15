---
title: 'MiniportPause \_ 返回规则 (ndis) '
description: MiniportPause \_ 返回规则指定，如果暂停操作完成，则 MiniportPause 回调函数应仅返回 ndis \_ 状态 \_ 成功; \_ \_ 如果微型端口驱动程序处于暂停状态，则为 ndis 状态。
ms.assetid: f3751636-6ba2-4126-88e2-1f347bd7dd45
ms.date: 05/21/2018
keywords:
- 'MiniportPause_Return 规则 (ndis) '
topic_type:
- apiref
api_name:
- MiniportPause_Return
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6494b3c64cc5ea84acdc74057f6181f67a922b0c
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105464"
---
# <a name="miniportpause_return-rule-ndis"></a>MiniportPause \_ 返回规则 (ndis) 


**MiniportPause \_ 返回**规则指定，如果暂停操作完成，则[*MiniportPause*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)回调函数应仅返回 ndis \_ 状态 \_ 成功; \_ \_ 如果微型端口驱动程序处于暂停状态，则为 ndis 状态。 任何其他返回的状态均无效。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>MiniportPause_Return</strong> 规则。</p>
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

