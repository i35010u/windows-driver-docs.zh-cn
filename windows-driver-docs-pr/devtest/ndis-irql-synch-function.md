---
title: Irql\_同步\_函数规则 (ndis)
description: Irql\_同步\_函数规则指定的 NDIS 中断和同步 DDIs 必须调用在正确的 IRQL 级别。
ms.assetid: 5d0e862a-89e6-493d-a102-83430c5140e4
ms.date: 05/21/2018
keywords:
- Irql_Synch_Function 规则 (ndis)
topic_type:
- apiref
api_name:
- Irql_Synch_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f34463959973602e0f6433dc3b820bc53bf72f8e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577355"
---
# <a name="irqlsynchfunction-rule-ndis"></a>Irql\_同步\_函数规则 (ndis)


**Irql\_同步\_函数**规则指定的 NDIS 中断和同步 DDIs 必须调用在正确的 IRQL 级别。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>Irql_Synch_Function</strong>规则。</p>
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

[**NDIS\_发行\_MUTEX**](https://msdn.microsoft.com/library/windows/hardware/ff567247)
[**NDIS\_等待\_为\_互斥体**](https://msdn.microsoft.com/library/windows/hardware/ff567897)
 [ **NdisAcquireReadWriteLock**](https://msdn.microsoft.com/library/windows/hardware/ff560696)
[**NdisAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff560699) 
 [ **NdisDprAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff561749)
[**NdisDprReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff561753) 
 [**NdisReleaseReadWriteLock**](https://msdn.microsoft.com/library/windows/hardware/ff564521)
[**NdisReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff564524) 
 [ **NdisResetEvent**](https://msdn.microsoft.com/library/windows/hardware/ff564526)
[**NdisSetEvent**](https://msdn.microsoft.com/library/windows/hardware/ff564539)
 

 





