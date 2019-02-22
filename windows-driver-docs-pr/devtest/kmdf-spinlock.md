---
title: 旋转锁规则 (kmdf)
description: 旋转锁规则指定对 KeAcquireSpinLock 或 KeAcquireSpinLockRaiseToDpc 和 KeReleaseSpinlock 调用可在严格的分支结构。
ms.assetid: 911E4350-851F-4AC4-B982-B2B4B974C243
ms.date: 05/21/2018
keywords:
- 旋转锁规则 (kmdf)
topic_type:
- apiref
api_name:
- Spinlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b8c7e765a70990080b7aa5bfaae7cdccca1af5be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546531"
---
# <a name="spinlock-rule-kmdf"></a>旋转锁规则 (kmdf)


**Spinlock**规则指定的调用[ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)或者[ **KeAcquireSpinLockRaiseToDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff551928)并[ **KeReleaseSpinlock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145)严格的分支结构中使用。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>旋转锁</strong>规则。</p>
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

[**KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)
[**KeAcquireSpinLockRaiseToDpc**](https://msdn.microsoft.com/library/windows/hardware/ff551928)
[**KeReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553145)
 

 





