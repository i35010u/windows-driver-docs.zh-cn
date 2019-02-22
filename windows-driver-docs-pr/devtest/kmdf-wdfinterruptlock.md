---
title: WdfInterruptLock 规则 (kmdf)
description: WdfInterruptLock 规则指定对 WdfInterruptAcquireLock 方法的调用在通过调用 WdfInterruptReleaseLock 严格替换中使用。
ms.assetid: bf105e83-dc63-44b1-ba9d-e4d81210fa1a
ms.date: 05/21/2018
keywords:
- WdfInterruptLock 规则 (kmdf)
topic_type:
- apiref
api_name:
- WdfInterruptLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 85d26cc7d753a9b0745509a4cc38bd811a2043d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546903"
---
# <a name="wdfinterruptlock-rule-kmdf"></a>WdfInterruptLock 规则 (kmdf)


**WdfInterruptLock**规则指定的调用[ **WdfInterruptAcquireLock** ](https://msdn.microsoft.com/library/windows/hardware/ff547340)严格逻辑或调用中使用方法[ **WdfInterruptReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff547376)。 此外，在任何 KMDF 回调例程结束时，该驱动程序不应阻止 framework 数值调节钮锁对象，通过以前调用获得**WdfInterruptAcquireLock**。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>WdfInterruptLock</strong>规则。</p>
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

[**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)
[**WdfInterruptReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff547376)
 

 





