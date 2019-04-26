---
title: MiniportPause\_返回规则 (ndis)
description: MiniportPause\_返回规则指定 MiniportPause 回调函数应返回仅 NDIS\_状态\_成功如果暂停操作已完成或 NDIS\_状态\_如果挂起微型端口驱动程序处于暂停状态。
ms.assetid: f3751636-6ba2-4126-88e2-1f347bd7dd45
ms.date: 05/21/2018
keywords:
- MiniportPause_Return 规则 (ndis)
topic_type:
- apiref
api_name:
- MiniportPause_Return
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 309fda71bbca15d2828b02ad85c80b644437c6ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327228"
---
# <a name="miniportpausereturn-rule-ndis"></a>MiniportPause\_返回规则 (ndis)


**MiniportPause\_返回**规则指定[ *MiniportPause* ](https://msdn.microsoft.com/library/windows/hardware/ff559418)回调函数应返回仅 NDIS\_状态\_如果暂停操作已完成，则为 SUCCESS 或 NDIS\_状态\_PENDING 微型端口驱动程序是否处于暂停状态。 其他任何返回的状态无效。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>MiniportPause_Return</strong>规则。</p>
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

 

 





