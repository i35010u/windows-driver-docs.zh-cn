---
title: WdfInterruptLockRelease 规则 (kmdf)
description: WdfInterruptLockRelease 规则指定对 WdfInterruptAcquireLock 和 WdfInterruptReleaseLock 的调用使用 KMDF 回调例程中以平衡方式。
ms.assetid: 2cad3811-99c2-4909-bad6-54cab9f006e6
ms.date: 05/21/2018
keywords:
- WdfInterruptLockRelease 规则 (kmdf)
topic_type:
- apiref
api_name:
- WdfInterruptLockRelease
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 53e4917f56253a328731f92a3d9b827a4b8a6176
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374744"
---
# <a name="wdfinterruptlockrelease-rule-kmdf"></a>WdfInterruptLockRelease 规则 (kmdf)


**WdfInterruptLockRelease**规则指定的调用[ **WdfInterruptAcquireLock** ](https://msdn.microsoft.com/library/windows/hardware/ff547340)并[ **WdfInterruptReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff547376) KMDF 回调例程中以平衡方式使用。 在任何 KMDF 回调例程结束时，该驱动程序不应阻止通过以前调用获得的 framework 自旋锁对象**WdfInterruptAcquireLock**。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>WdfInterruptLockRelease</strong>规则。</p>
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

[**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)
[**WdfInterruptReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff547376)
 

 





