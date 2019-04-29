---
title: PdoInitFreeDeviceCreateType4 规则 (kmdf)
description: PdoInitFreeDeviceCreateType4 规则指定是否驱动程序调用 WdfDeviceCreate 时发生错误，该驱动程序必须调用 WdfDeviceInitFree。
ms.assetid: 9293f293-7de6-476a-ab35-09174b7b3480
ms.date: 05/21/2018
keywords:
- PdoInitFreeDeviceCreateType4 规则 (kmdf)
topic_type:
- apiref
api_name:
- PdoInitFreeDeviceCreateType4
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 24ff7cb0c9ee3de74373f08a1bd017cb086ecc79
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384097"
---
# <a name="pdoinitfreedevicecreatetype4-rule-kmdf"></a>PdoInitFreeDeviceCreateType4 规则 (kmdf)


PdoInitFreeDeviceCreateType4 规则指定驱动程序必须调用[ **WdfDeviceInitFree** ](https://msdn.microsoft.com/library/windows/hardware/ff546050)如果驱动程序调用出错[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926).

如果您的驱动程序时遇到错误时它将调用[ **WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)，并且如果该驱动程序收到[WDFDEVICE\_INIT](https://msdn.microsoft.com/library/windows/hardware/ff546951) 调用的结构[**WdfPdoInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff548786)，该驱动程序必须调用[ **WdfDeviceInitFree**](https://msdn.microsoft.com/library/windows/hardware/ff546050)。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>PdoInitFreeDeviceCreateType4</strong>规则。</p>
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

[**WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)
[**WdfDeviceInitFree**](https://msdn.microsoft.com/library/windows/hardware/ff546050)
[**WdfPdoInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff548786)
 

 





