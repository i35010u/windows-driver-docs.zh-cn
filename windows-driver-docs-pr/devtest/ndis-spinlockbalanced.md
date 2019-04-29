---
title: SpinLockBalanced 规则 (ndis)
description: SpinLockBalanced 规则验证获取调节锁的函数的调用的数量与发布相同的旋转锁的函数的调用的数相等。
ms.assetid: 61abb66e-b271-4102-828b-7e5ce77295c4
ms.date: 05/21/2018
keywords:
- SpinLockBalanced 规则 (ndis)
topic_type:
- apiref
api_name:
- SpinLockBalanced
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bd7289b5bd27f886c02cada8d79d7263f7627f70
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354345"
---
# <a name="spinlockbalanced-rule-ndis"></a>SpinLockBalanced 规则 (ndis)


**SpinLockBalanced**规则验证获取调节锁的函数的调用的数量是否与发布相同的旋转锁的函数的调用的数相等。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>SpinLockBalanced</strong>规则。</p>
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

[**NdisAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff560699)
[**NdisDprAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff561749)
[**NdisDprReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff561753)
[**NdisReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff564524)
 

 





