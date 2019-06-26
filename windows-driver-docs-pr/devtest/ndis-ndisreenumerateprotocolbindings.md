---
title: NdisReEnumerateProtocolBindings 规则 (ndis)
description: 协议驱动程序不能调用从 NdisReEnumerateProtocolBindings ProtocolBindAdapterEx 或 ProtocolUnbindAdapterEx 函数的上下文中。
ms.assetid: A6BB5B25-B8F4-4D90-B325-DFEED9C4AA6A
ms.date: 05/21/2018
keywords:
- NdisReEnumerateProtocolBindings 规则 (ndis)
topic_type:
- apiref
api_name:
- NdisReEnumerateProtocolBindings
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0df3af123cbc7360d9d69d15b76fd8dfa888ff50
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392203"
---
# <a name="ndisreenumerateprotocolbindings-rule-ndis"></a>NdisReEnumerateProtocolBindings 规则 (ndis)


协议驱动程序不能调用[ **NdisReEnumerateProtocolBindings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreenumerateprotocolbindings)中的上下文中[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)或[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)函数。 此外，协议驱动程序不能调用**NdisReEnumerateProtocolBindings**中的上下文中[ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)函数如果*ProtocolBindingContext*的参数*ProtocolNetPnPEvent*不为 NULL。 但是，协议驱动程序可以调用**NdisReEnumerateProtocolBindings**中的上下文中*ProtocolNetPnPEvent*如果*ProtocolBindingContext*为 NULL。 为空*ProtocolBindingContext*值指示该事件适用于所有绑定。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>NdisReEnumerateProtocolBindings</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**NdisReEnumerateProtocolBindings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreenumerateprotocolbindings)
 

 





