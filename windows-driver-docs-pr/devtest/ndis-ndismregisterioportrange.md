---
title: NdisMRegisterIoPortRange 规则 (ndis)
description: 微型端口驱动程序从其 MiniportInitializeEx 或微型端口调用 NdisMRegisterIoPortRange\_添加\_设备函数。 MiniportInitializeEx 或微型端口\_添加\_设备之前必须先调用 NdisMSetMiniportAttributes 调用 NdisMRegisterIoPortRange。
ms.assetid: 74CFCBDB-3044-4447-ABEF-A60BA31C0BE0
ms.date: 05/21/2018
keywords:
- NdisMRegisterIoPortRange 规则 (ndis)
topic_type:
- apiref
api_name:
- NdisMRegisterIoPortRange
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: abba4de6b4bfed51ddcb75cd75f1329641f43ebc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362303"
---
# <a name="ndismregisterioportrange-rule-ndis"></a>NdisMRegisterIoPortRange 规则 (ndis)


微型端口驱动程序调用[ **NdisMRegisterIoPortRange** ](https://msdn.microsoft.com/library/windows/hardware/ff563651)从其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)或微型端口\_添加\_设备函数。 *MiniportInitializeEx*或微型端口\_添加\_设备必须调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)之前调用**NdisMRegisterIoPortRange**。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>NdisMRegisterIoPortRange</strong>规则。</p>
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

[**NdisMRegisterIoPortRange**](https://msdn.microsoft.com/library/windows/hardware/ff563651)
[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)
 

 





