---
title: ObsoleteDDIs 规则 (wdm)
description: ObsoleteDDIs 规则指定驱动程序不应调用 FsRtlPrivateLock。 此函数已过时。 请改用 FsRtlFastLock。
ms.assetid: 5C49270A-7AD1-4762-921E-7925006D0400
ms.date: 05/21/2018
keywords:
- ObsoleteDDIs 规则 (wdm)
topic_type:
- apiref
api_name:
- ObsoleteDDIs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d7ac4d0ae62446963cf23b793c086f589b65e344
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547227"
---
# <a name="obsoleteddis-rule-wdm"></a>ObsoleteDDIs 规则 (wdm)


**ObsoleteDDIs**规则指定驱动程序不应调用[ **FsRtlPrivateLock**](https://msdn.microsoft.com/library/windows/hardware/ff547164)。 此函数已过时。 使用[ **FsRtlFastLock** ](https://msdn.microsoft.com/library/windows/hardware/ff545940)相反。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>ObsoleteDDIs</strong>规则。</p>
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

 

 





