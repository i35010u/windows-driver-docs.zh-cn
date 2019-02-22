---
title: NdisMMapIoSpace 规则 (ndis)
description: 仅应 MiniportInitializeEx 的上下文中调用 NdisMMapIoSpace 函数。
ms.assetid: C93420DB-ADB3-4C99-8D57-059B4650308D
ms.date: 05/21/2018
keywords:
- NdisMMapIoSpace 规则 (ndis)
topic_type:
- apiref
api_name:
- NdisMMapIoSpace
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2c62b96c4650ec1a7f83353562a8f3f8ab77c9cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555086"
---
# <a name="ndismmapiospace-rule-ndis"></a>NdisMMapIoSpace 规则 (ndis)


[ **NdisMMapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/ff563613)函数只应调用的上下文中[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>NdisMMapIoSpace</strong>规则。</p>
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

[**NdisMMapIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff563613)
 

 





