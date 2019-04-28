---
title: SpinLockDpr 规则 (ndis)
description: SpinLockDpr 规则验证 NDIS 数值调节钮锁定接口的正确用法。此规则指定仅当自旋锁处于解锁状态时进行调用 NdisDprAcquireSpinLock。
ms.assetid: 60056fae-54d1-4365-bcb5-02c63e4fb521
ms.date: 05/21/2018
keywords:
- SpinLockDpr 规则 (ndis)
topic_type:
- apiref
api_name:
- SpinLockDpr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ccc731b8132b307a48509fe41271f7a98c743c94
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327524"
---
# <a name="spinlockdpr-rule-ndis"></a>SpinLockDpr 规则 (ndis)


**SpinLockDpr**规则验证 NDIS 数值调节钮锁定接口的正确用法。

此规则指定的调用[ **NdisDprAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff561749)只有自旋锁处于解锁状态时进行。 此规则还会验证微型端口处理程序例程退出之前释放自旋锁。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>SpinLockDpr</strong>规则。</p>
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
[**NdisAllocateSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff561617)
[**NdisDprAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff561749)
[**NdisDprReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff561753)
[**NdisReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff564524)
 

 





