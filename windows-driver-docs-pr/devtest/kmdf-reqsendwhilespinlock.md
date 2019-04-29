---
title: ReqSendWhileSpinlock 规则 (kmdf)
description: ReqSendWhileSpinlock 规则指定驱动程序包含自旋锁时发送了任何请求。
ms.assetid: f038f4ca-aa24-4df3-9c31-d8eec928c306
ms.date: 05/21/2018
keywords:
- ReqSendWhileSpinlock 规则 (kmdf)
topic_type:
- apiref
api_name:
- ReqSendWhileSpinlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c9b08f4071a5973f9efdb38daa54798bfd9af829
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368662"
---
# <a name="reqsendwhilespinlock-rule-kmdf"></a>ReqSendWhileSpinlock 规则 (kmdf)


**ReqSendWhileSpinlock**规则指定驱动程序包含自旋锁时发送了任何请求。

如果旋转锁时，该驱动程序发送的任何请求，它可能导致死锁，或者如果较低的驱动程序还会尝试获取锁或访问共享的资源的较低的驱动程序接收请求，发生冲突。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>ReqSendWhileSpinlock</strong>规则。</p>
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

[**WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)
[**WdfSpinLockAcquire**](https://msdn.microsoft.com/library/windows/hardware/ff550040)
[**WdfSpinLockRelease**](https://msdn.microsoft.com/library/windows/hardware/ff550044) 
 [ **KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)
[**KeReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145)请参阅还
--------

[完成 I/O 请求](https://msdn.microsoft.com/library/windows/hardware/ff540740)
[同步取消和完成代码](https://msdn.microsoft.com/library/windows/hardware/ff544726)
 

 





