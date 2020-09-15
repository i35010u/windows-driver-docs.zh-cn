---
title: 'StorPortFindAdapter 规则 (storport) '
description: HwStorFindAdapter 例程必须在端口 \_ 配置信息结构中设置 MaximumTransferLength 和 NumberOfPhysicalBreaks 字段 \_ 。
ms.assetid: 8BE79E99-078E-4CCE-A6C1-0DEB1F1252DA
ms.date: 05/21/2018
keywords:
- 'StorPortFindAdapter 规则 (storport) '
topic_type:
- apiref
api_name:
- StorPortFindAdapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ebaa10675b2af0da4a0bddad7d842474d989ca83
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105240"
---
# <a name="storportfindadapter-rule-storport"></a>StorPortFindAdapter 规则 (storport) 


[**HwStorFindAdapter**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)例程必须在**端口 \_ 配置 \_ 信息**结构中设置**MaximumTransferLength**和**NumberOfPhysicalBreaks**字段。 默认情况下，这两个字段的值均为 **SP \_ 未初始化 \_ 值**。 如果在退出**FindAdapter**时，这些字段中的任一字段仍设置为** \_ 未初始化的 SP \_ 值**，则驱动程序将无法通过该规则。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>StorPortFindAdapter</strong> 规则。</p>
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

