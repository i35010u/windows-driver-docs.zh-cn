---
title: IoAllocateForward 规则 (wdm)
description: IoAllocateForward 规则指定，是否通过调用 IoAllocateIrp 生成 IRP，则驱动程序必须在调用 IoCallDriver 或 PoCallDriver 之前设置完成例程。
ms.assetid: 5FA404C9-B5FD-47DA-9F9D-14C8F269B6A4
ms.date: 05/21/2018
keywords:
- IoAllocateForward 规则 (wdm)
topic_type:
- apiref
api_name:
- IoAllocateForward
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 74ca8582ea831b4a9c7856b25b78e23032e8d7e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365064"
---
# <a name="ioallocateforward-rule-wdm"></a>IoAllocateForward 规则 (wdm)


**IoAllocateForward**规则指定如果通过调用生成 IRP [ **IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)，驱动程序必须调用之前设置完成例程[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)或[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IoAllocateForward</strong>规则。</p>
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

[**IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)
[**IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)
[**IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





