---
title: SyncReqSend2 规则 (kmdf)
description: SyncReqSend2 规则指定同步请求发送具有非零的超时值设置。
ms.assetid: c72b909f-6160-47da-8e7e-84e0dea785c2
ms.date: 05/21/2018
keywords:
- SyncReqSend2 规则 (kmdf)
topic_type:
- apiref
api_name:
- SyncReqSend2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3f9776cb9b0bda5cd74b9507755acc425c2b5a8c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555870"
---
# <a name="syncreqsend2-rule-kmdf"></a>SyncReqSend2 规则 (kmdf)


**SyncReqSend2**规则指定同步请求发送具有非零的超时值设置。

如果该驱动程序调用[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)而无需在请求选项中设置的有效超时值，如果没有立即响应硬件可以停止该线程。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>SyncReqSend2</strong>规则。</p>
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

[**WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)
 

 





