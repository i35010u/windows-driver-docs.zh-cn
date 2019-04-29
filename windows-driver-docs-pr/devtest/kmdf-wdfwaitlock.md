---
title: WdfWaitlock 规则 (kmdf)
description: WdfWaitlock 规则指定 WdfWaitLockAcquire 对的调用在与 WdfWaitlockRelease 严格替换中使用。
ms.assetid: 481c5a21-6c4d-41e3-a54a-3da07d287fda
ms.date: 05/21/2018
keywords:
- WdfWaitlock 规则 (kmdf)
topic_type:
- apiref
api_name:
- WdfWaitlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 196b38553fa1b83664ab7b1c2ebc5f9900fd0741
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374735"
---
# <a name="wdfwaitlock-rule-kmdf"></a>WdfWaitlock 规则 (kmdf)


**WdfWaitlock**规则指定的调用[ **WdfWaitLockAcquire** ](https://msdn.microsoft.com/library/windows/hardware/ff551168)可在使用逻辑或 strict [ **WdfWaitlockRelease**](kmdf-wdfwaitlockrelease.md). KMDF 事件回调函数返回时，该驱动程序不应阻止通过以前调用获得的 framework 自旋锁对象**WdfWaitLockAcquire**。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>WdfWaitlock</strong>规则。</p>
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

[**WdfWaitLockAcquire**](https://msdn.microsoft.com/library/windows/hardware/ff551168)
[**WdfWaitLockRelease**](https://msdn.microsoft.com/library/windows/hardware/ff551173)
 

 





