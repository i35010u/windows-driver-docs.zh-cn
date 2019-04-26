---
title: IoReuseIrp 规则 (wdm)
description: IoReuseIrp 规则指定一个驱动程序应仅在使用 IoAllocateIrp 以前分配的 Irp 上使用 IoReuseIrp。
ms.assetid: E927D12D-03DE-41D7-B130-BA86F0C0CB8A
ms.date: 05/21/2018
keywords:
- IoReuseIrp 规则 (wdm)
topic_type:
- apiref
api_name:
- IoReuseIrp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1cdad946e603a13c2a1325e5e92bc9c4853f1e35
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325344"
---
# <a name="ioreuseirp-rule-wdm"></a>IoReuseIrp 规则 (wdm)


**IoReuseIrp**规则指定一个驱动程序应使用[ **IoReuseIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549661)仅在使用以前分配的 Irp 上[ **IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IoReuseIrp</strong>规则。</p>
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

[**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397)
[**ExInterlockedInsertTailList** ](https://msdn.microsoft.com/library/windows/hardware/ff545402) 
 [ **ExInterlockedPushEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545418)
[**InsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff547820)
[**IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257) 
 [ **IoCsqInsertIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549066)
[**IoCsqInsertIrpEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549067)
 [ **IoInitializeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549315)
[**IoReuseIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549661) 
 [ **RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)
 

 





