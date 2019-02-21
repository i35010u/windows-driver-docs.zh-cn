---
title: Init\_RegisterSG 规则 (ndis)
description: Init\_RegisterSG 规则指定，是否出现问题或过程的微型端口停止初始化过程中，通常发生在初始化期间，分散-集中列表 (SG) 的注册必须是撤消驱动程序。如果 NdisMRegisterScatterGatherDma 调用 MiniportInitializeEx 至少一次，NdisMDeregisterScatterGatherDma 函数应在 MiniportHaltEx 调用至少一次。
ms.assetid: c4d00be1-b44b-4769-bbe6-6128a742d088
ms.date: 05/21/2018
keywords:
- Init_RegisterSG 规则 (ndis)
topic_type:
- apiref
api_name:
- Init_RegisterSG
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d96e58d87328d61b7c4ff0733b45472880c81806
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542777"
---
# <a name="initregistersg-rule-ndis"></a>Init\_RegisterSG 规则 (ndis)


Init\_RegisterSG 规则指定，是否出现问题或过程的微型端口停止初始化过程中，通常发生在初始化期间，分散-集中列表 (SG) 的注册必须是撤消驱动程序。

如果**NdisMRegisterScatterGatherDma**称为至少一次**MiniportInitializeEx**，则**NdisMDeregisterScatterGatherDma**必须在调用函数中的至少一次**MiniportHaltEx**。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>Init_RegisterSG</strong>规则。</p>
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

<a name="applies-to"></a>适用于
----------

[**NdisMDeregisterScatterGatherDma**](https://msdn.microsoft.com/library/windows/hardware/ff563581)
[**NdisMRegisterScatterGatherDma**](https://msdn.microsoft.com/library/windows/hardware/ff563659)
 

 





