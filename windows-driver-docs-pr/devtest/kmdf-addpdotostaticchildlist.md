---
title: AddPdotoStaticChildlist 规则 (kmdf)
description: AddPdotoStaticChildlist 规则指定，对于 PDO 设备，framework 函数 WdfFdoAddStaticChild 之后必须调用该驱动程序已成功调用 WdfPdoInitAllocate 和 WdfDeviceCreate。
ms.assetid: 31ECB3D2-1EAC-484A-8C3A-DF94AC473334
ms.date: 05/21/2018
keywords:
- AddPdotoStaticChildlist 规则 (kmdf)
topic_type:
- apiref
api_name:
- AddPdotoStaticChildlist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f233826984e174d3b7222d2ff1c6d8ef921a5e64
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356457"
---
# <a name="addpdotostaticchildlist-rule-kmdf"></a>AddPdotoStaticChildlist 规则 (kmdf)


AddPdotoStaticChildlist 规则指定 PDO 设备，framework 函数[ **WdfFdoAddStaticChild** ](https://msdn.microsoft.com/library/windows/hardware/ff547225)驱动程序调用后，必须调用[ **WdfPdoInitAllocate** ](https://msdn.microsoft.com/library/windows/hardware/ff548786)并[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)成功。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>AddPdotoStaticChildlist</strong>规则。</p>
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
[**WdfFdoAddStaticChild**](https://msdn.microsoft.com/library/windows/hardware/ff547225)
[**WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)
[**WdfPdoInitAllocate**](https://msdn.microsoft.com/library/windows/hardware/ff548786)
 

 





