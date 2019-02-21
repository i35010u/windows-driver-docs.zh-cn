---
title: FDOPowerPolicyOwnerAPI 规则 (kmdf)
description: FDOPowerPolicyOwnerAPI 规则指定，是否 FDO 驱动程序将放弃电源策略所有权，WdfDeviceInitSetPowerPolicyEventCallbacks、 WdfDeviceAssignS0IdleSettings 和 WdfDeviceAssignSxWakeSettings 可以仅在上调用方法其中的驱动程序是电源策略所有者的执行路径。 SDV 发出对此规则的警告。
ms.assetid: b0695dff-070c-4c55-a71d-a78fc45eb805
ms.date: 05/21/2018
keywords:
- FDOPowerPolicyOwnerAPI 规则 (kmdf)
topic_type:
- apiref
api_name:
- FDOPowerPolicyOwnerAPI
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d4d3bb8e4f57344b96e22e4a4d2eaf73751732c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520412"
---
# <a name="fdopowerpolicyownerapi-rule-kmdf"></a>FDOPowerPolicyOwnerAPI 规则 (kmdf)


**FDOPowerPolicyOwnerAPI**规则指定，如果 FDO 驱动程序将放弃电源策略所有权，方法[ **WdfDeviceInitSetPowerPolicyEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546774)， [ **WdfDeviceAssignS0IdleSettings**](https://msdn.microsoft.com/library/windows/hardware/ff545903)，并[ **WdfDeviceAssignSxWakeSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff545909)只能上调用其中的驱动程序是电源策略所有者的执行路径。 SDV 发出对此规则的警告。

如果 FDO 驱动程序调用[ **WdfDeviceInitSetPowerPolicyOwnership** ](https://msdn.microsoft.com/library/windows/hardware/ff546776)方法替换**FALSE**作为值的第二个参数，随后只要调用[ **WdfDeviceInitSetPowerPolicyEventCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff546774)， **WdfDeviceAssignS0IdleSettings**，和**WdfDeviceAssignSxWakeSettings**该驱动程序将导致规则冲突和警告消息。

|              |      |
|--------------|------|
| 驱动程序模型 | KMDF |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>FDOPowerPolicyOwnerAPI</strong>规则。</p>
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

[**WdfDeviceAssignS0IdleSettings**](https://msdn.microsoft.com/library/windows/hardware/ff545903)
[**WdfDeviceAssignSxWakeSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff545909) 
 [ **WdfDeviceInitSetPowerPolicyEventCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff546774)
[**WdfDeviceInitSetPowerPolicyOwnership**](https://msdn.microsoft.com/library/windows/hardware/ff546776)
 

 





