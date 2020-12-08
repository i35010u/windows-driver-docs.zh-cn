---
title: 'SpReturnValue 规则 (storport) '
description: 此规则验证驱动程序的 HwStorFindAdapter 和 VirtualHwStorFindAdapter 实现是否返回有效状态。 有效状态为以下某个 SP \_ 返回 \_ ，sp \_ 返回 \_ 错误，sp \_ 返回错误 \_ \_ 配置，或者 \_ \_ 找不到 sp 返回 \_ 。
ms.date: 05/21/2018
keywords:
- 'SpReturnValue 规则 (storport) '
topic_type:
- apiref
api_name:
- SpReturnValue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 93ed6e980fe52c2c34293abb432598302befd665
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828149"
---
# <a name="spreturnvalue-rule-storport"></a>SpReturnValue 规则 (storport) 


此规则验证驱动程序的 [**HwStorFindAdapter**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter) 和 [**VirtualHwStorFindAdapter**](/windows-hardware/drivers/ddi/storport/nc-storport-virtual_hw_find_adapter) 实现是否返回有效状态。 有效状态为以下状态之一：已 **\_ \_ 找到 sp**，sp 返回 **\_ \_ 错误**， **Sp 返回错误 \_ \_ \_ 配置**，或 **\_ \_ \_ 找不到 sp 返回**。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>SpReturnValue</strong> 规则。</p>
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

