---
title: 'Init \_ RegisterSG rule (ndis) '
description: Init \_ RegisterSG 规则指定，如果在初始化过程中出现问题或在停止微型端口驱动程序的过程中出现问题，则在初始化期间 (SG) 的分散收集列表的注册必须撤消。如果在 MiniportInitializeEx 期间至少调用了一次 NdisMRegisterScatterGatherDma，则 NdisMDeregisterScatterGatherDma 函数应在 MiniportHaltEx 中至少调用一次。
ms.assetid: c4d00be1-b44b-4769-bbe6-6128a742d088
ms.date: 05/21/2018
keywords:
- 'Init_RegisterSG 规则 (ndis) '
topic_type:
- apiref
api_name:
- Init_RegisterSG
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8976d44a697740e3db98284148637d99b8d1a148
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105318"
---
# <a name="init_registersg-rule-ndis"></a>Init \_ RegisterSG rule (ndis) 


Init \_ RegisterSG 规则指定，如果在初始化过程中出现问题或在停止微型端口驱动程序的过程中出现问题，则在初始化期间 (SG) 的分散收集列表的注册必须撤消。

如果在**MiniportInitializeEx**期间至少调用了一次**NdisMRegisterScatterGatherDma** ，则**NdisMDeregisterScatterGatherDma**函数应在**MiniportHaltEx**中至少调用一次。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>Init_RegisterSG</strong> 规则。</p>
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

[**NdisMDeregisterScatterGatherDma**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterscattergatherdma) 
[ **NdisMRegisterScatterGatherDma**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterscattergatherdma)
