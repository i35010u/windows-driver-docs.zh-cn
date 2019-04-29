---
title: StorPortDeprecated 规则 (storport)
description: 此规则验证，该驱动程序不会调用任何一种方法已弃用 StorPortValidateRange 或 StorPortLogError 例程。
ms.assetid: 90223719-91AB-4D10-88A0-0DBD2D99C5B2
ms.date: 05/21/2018
keywords:
- StorPortDeprecated 规则 (storport)
topic_type:
- apiref
api_name:
- StorPortDeprecated
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f5dc8f29ea293def1436f2d795dafb2a7b06c2dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362659"
---
# <a name="storportdeprecated-rule-storport"></a>StorPortDeprecated 规则 (storport)


此规则验证，该驱动程序不会调用这些不推荐使用的例程之一：**StorPortValidateRange**或**StorPortLogError**。

|              |          |
|--------------|----------|
| 驱动程序模型 | Storport |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>StorPortDeprecated</strong>规则。</p>
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

[**StorPortLogError**](https://msdn.microsoft.com/library/windows/hardware/ff567426)
[**StorPortValidateRange**](https://msdn.microsoft.com/library/windows/hardware/ff567513)
 

 





