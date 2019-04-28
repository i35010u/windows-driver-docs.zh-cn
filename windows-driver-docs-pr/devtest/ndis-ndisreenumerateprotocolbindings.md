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
ms.openlocfilehash: 2b020ec0c65b64e3dd75e7e607d31c51889c48fc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327531"
---
# <a name="ndisreenumerateprotocolbindings-rule-ndis"></a>NdisReEnumerateProtocolBindings 规则 (ndis)


协议驱动程序不能调用[ **NdisReEnumerateProtocolBindings** ](https://msdn.microsoft.com/library/windows/hardware/ff564516)中的上下文中[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)或[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)函数。 此外，协议驱动程序不能调用**NdisReEnumerateProtocolBindings**中的上下文中[ *ProtocolNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff570263)函数如果*ProtocolBindingContext*的参数*ProtocolNetPnPEvent*不为 NULL。 但是，协议驱动程序可以调用**NdisReEnumerateProtocolBindings**中的上下文中*ProtocolNetPnPEvent*如果*ProtocolBindingContext*为 NULL。 为空*ProtocolBindingContext*值指示该事件适用于所有绑定。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>NdisReEnumerateProtocolBindings</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**NdisReEnumerateProtocolBindings**](https://msdn.microsoft.com/library/windows/hardware/ff564516)
 

 





