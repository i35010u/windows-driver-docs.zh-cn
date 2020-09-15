---
title: 'NdisAllocateNetBuffer 规则 (ndis) '
description: NdisAllocateNetBuffer 规则指定按替代顺序调用 NdisAllocateNetBuffer 和 NdisFreeNetBuffer。 最终的目标是确保 \_ 在 MiniportHaltEx 结束时释放 NET BUFFER 的所有实例。
ms.assetid: 218708DA-ADDF-4E59-900A-4F8B5CBF00B7
ms.date: 05/21/2018
keywords:
- 'NdisAllocateNetBuffer 规则 (ndis) '
topic_type:
- apiref
api_name:
- NdisAllocateNetBuffer
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 79dd991281d61501436b6d0f2db9a002e68847c8
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105452"
---
# <a name="ndisallocatenetbuffer-rule-ndis"></a>NdisAllocateNetBuffer 规则 (ndis) 


**NdisAllocateNetBuffer**规则指定按替代顺序调用[**NdisAllocateNetBuffer**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbuffer)和[**NdisFreeNetBuffer**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer) 。 最终的目标是确保在[*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)结束时释放[**NET \_ BUFFER**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)的所有实例。

此规则使用三种不同的状态。 当分配或释放 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 时，状态将更改。 如果在[*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)退出时仍分配**网络 \_ 缓冲区**，则规则将报告缺陷。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>NdisAllocateNetBuffer</strong> 规则。</p>
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

[**NdisAllocateNetBuffer**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocatenetbuffer) 
[ **NdisFreeNetBuffer**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreenetbuffer)
