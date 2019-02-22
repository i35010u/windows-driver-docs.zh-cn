---
title: IoSetCompletionRoutineNonPnpDriver 规则 (wdm)
description: IoSetCompletionRoutineNonPnpDriver 规则指定驱动程序不是即插即用驱动程序应使用 IoSetCompletionRoutineEx 不 IoSetCompletionRoutine。
ms.assetid: E4C6415B-DCB5-4AE2-9112-BC314D443C73
ms.date: 05/21/2018
keywords:
- IoSetCompletionRoutineNonPnpDriver 规则 (wdm)
topic_type:
- apiref
api_name:
- IoSetCompletionRoutineNonPnpDriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3414ef9752b0eb650ea2e6f1cb3fa67e81716bcc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522594"
---
# <a name="iosetcompletionroutinenonpnpdriver-rule-wdm"></a>IoSetCompletionRoutineNonPnpDriver 规则 (wdm)


**IoSetCompletionRoutineNonPnpDriver**规则指定驱动程序不是即插即用驱动程序应使用[ **IoSetCompletionRoutineEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549686)不[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)。

[ **IoSetCompletionRoutineEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549686)例程避免了实际的驱动程序映像，卸载后已标记为要卸载该驱动程序。 这适用于非 PnP 驱动程序，因为它们不会通知即插即用的管理器时删除或卸载正在发生的情况。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IoSetCompletionRoutineNonPnpDriver</strong>规则。</p>
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

[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)
 

 





