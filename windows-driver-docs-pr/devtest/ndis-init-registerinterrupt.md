---
title: Init\_RegisterInterrupt 规则 (ndis)
description: Init\_RegisterInterrupt 规则指定，是否出现问题或过程停止微型端口驱动程序初始化过程中，注册中断，这通常发生在初始化期间，必须是撤消。如果 NdisMRegisterInterruptEx 调用 MiniportInitializeEx 至少一次，NdisMDeregisterInterruptEx 函数必须在 MiniportHaltEx 调用至少一次。
ms.assetid: f12cc1b9-396b-4351-ad13-c1750b54b709
ms.date: 05/21/2018
keywords:
- Init_RegisterInterrupt 规则 (ndis)
topic_type:
- apiref
api_name:
- Init_RegisterInterrupt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d06113268ccf06453eb774c94b205f1924808e7d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567221"
---
# <a name="initregisterinterrupt-rule-ndis"></a>Init\_RegisterInterrupt 规则 (ndis)


Init\_RegisterInterrupt 规则指定，是否出现问题或过程停止微型端口驱动程序初始化过程中，注册中断，这通常发生在初始化期间，必须是撤消。

如果**NdisMRegisterInterruptEx**称为至少一次**MiniportInitializeEx**，则**NdisMDeregisterInterruptEx**必须至少一次调用函数在中**MiniportHaltEx**。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>Init_RegisterInterrupt</strong>规则。</p>
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

[**NdisMDeregisterInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff563575)
[**NdisMRegisterInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff563649)
 

 





