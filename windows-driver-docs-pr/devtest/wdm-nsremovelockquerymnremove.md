---
title: NsRemoveLockQueryMnRemove 规则 (wdm)
description: NsRemoveLockQueryMnRemove 规则验证驱动程序不会返回状态\_不\_支持时处理 IRP\_MJ\_PNP 与 MinorFunction IRP\_MN\_查询\_中删除。 此规则仅适用于 FDO 和 FIDO 驱动程序。
ms.assetid: D6B22269-96D0-449A-B32D-F038D4AA065F
ms.date: 05/21/2018
keywords:
- NsRemoveLockQueryMnRemove 规则 (wdm)
topic_type:
- apiref
api_name:
- NsRemoveLockQueryMnRemove
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ecf9dd56a911e8899c6f763df26bdb2b98d2a01c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523365"
---
# <a name="nsremovelockquerymnremove-rule-wdm"></a>NsRemoveLockQueryMnRemove 规则 (wdm)


**NsRemoveLockQueryMnRemove**规则验证驱动程序不会返回状态\_不\_时处理 IRP，支持\_MJ\_PNP 与 MinorFunction IRP\_MN\_查询\_删除。 此规则仅适用于 FDO 和 FIDO 驱动程序。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>NsRemoveLockQueryMnRemove</strong>规则。</p>
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

[**IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)
 

 





