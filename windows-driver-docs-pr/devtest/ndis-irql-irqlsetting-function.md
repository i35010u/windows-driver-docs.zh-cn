---
title: Irql\_IrqlSetting\_函数规则 (ndis)
description: Irql\_IrqlSetting\_函数规则指定必须在正确的 IRQL 级别上名为 NDIS 中断宏。
ms.assetid: 47e62c7c-bd43-4b4a-b7d6-3f64a4b8a6c8
ms.date: 05/21/2018
keywords:
- Irql_IrqlSetting_Function 规则 (ndis)
topic_type:
- apiref
api_name:
- Irql_IrqlSetting_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 35bc1330fdafa1ee9d089b19157d45a2fdf18043
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370885"
---
# <a name="irqlirqlsettingfunction-rule-ndis"></a>Irql\_IrqlSetting\_函数规则 (ndis)


Irql\_IrqlSetting\_函数规则指定必须在正确的 IRQL 级别上名为 NDIS 中断宏。

此规则验证以下 NDIS 宏：

**NDIS\_LOWER\_IRQL**
**NDIS\_RAISE\_IRQL\_TO\_DISPATCH**

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>Irql_IrqlSetting_Function</strong>规则。</p>
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

[**NDIS\_LOWER\_IRQL**](https://msdn.microsoft.com/library/windows/hardware/ff565882)
[**NDIS\_RAISE\_IRQL\_TO\_DISPATCH**](https://msdn.microsoft.com/library/windows/hardware/ff566854)








