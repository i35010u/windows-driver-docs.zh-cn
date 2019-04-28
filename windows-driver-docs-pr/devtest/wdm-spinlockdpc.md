---
title: SpinLockDpc 规则 (wdm)
description: SpinLockDpc 规则指定必须在严格的分支结构中进行对 KeAcquireSpinLock 或 KeAcquireSpinLockRaiseToDpc 和 KeReleaseSpinLock 的调用。
ms.assetid: 24fa6db6-83b5-4586-8965-5dabdbc897d1
ms.date: 05/21/2018
keywords:
- SpinLockDpc 规则 (wdm)
topic_type:
- apiref
api_name:
- SpinLockDpc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4d9840ae013df73c62c27b207357903110f315a7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327142"
---
# <a name="spinlockdpc-rule-wdm"></a>SpinLockDpc 规则 (wdm)


**SpinLockDpc**规则指定的调用[ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)或者[ **KeAcquireSpinLockRaiseToDpc**](https://msdn.microsoft.com/library/windows/hardware/ff551928)并[ **KeReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145)必须在严格的分支结构中进行。 也就是说，之后调用**KeAcquireSpinLock**或**KeAcquireSpinLockRaiseToDpc**，该驱动程序必须调用**KeReleaseSpinLock**之前对的后续调用**KeAcquireSpinLock**或设置为**KeAcquireSpinLockRaiseToDpc**。

此外，在调度或取消例程结束时，该驱动程序不应阻止自旋锁。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>SpinLockDpc</strong>规则。</p>
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

[**KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)
[**KeAcquireSpinLockRaiseToDpc**](https://msdn.microsoft.com/library/windows/hardware/ff551928)
[**KeReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553145)
 

 





