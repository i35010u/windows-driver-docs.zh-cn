---
title: NdisMFreeSharedMemory 规则 (ndis)
description: 不能从 MiniportShutdownEx 函数调用 NdisMFreeSharedMemory。
ms.assetid: 86109F0F-38ED-4A20-9BFF-7738D7944DD8
ms.date: 05/21/2018
keywords:
- NdisMFreeSharedMemory 规则 (ndis)
topic_type:
- apiref
api_name:
- NdisMFreeSharedMemory
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d6a958b155866d14fe15bb7146ab94f06c453f28
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382704"
---
# <a name="ndismfreesharedmemory-rule-ndis"></a>NdisMFreeSharedMemory 规则 (ndis)


[**NdisMFreeSharedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff563589)不能从调用[ *MiniportShutdownEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559449)函数。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>NdisMFreeSharedMemory</strong>规则。</p>
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

[**NdisMFreeSharedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff563589)
 

 





