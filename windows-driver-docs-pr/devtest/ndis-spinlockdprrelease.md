---
title: SpinLockDprRelease 规则 (ndis)
description: SpinLockDprRelease 规则验证时，才释放调节锁称为调用 NdisAcquireSpinLock 或 NdisDprAcquireSpinLock \ 0034; 解除锁定 \ 0034;状态。
ms.assetid: B726B1AD-F49D-479B-AF1B-99E8901E2315
ms.date: 05/21/2018
keywords:
- SpinLockDprRelease 规则 (ndis)
topic_type:
- apiref
api_name:
- SpinLockDprRelease
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3e3d36857f389524d2d18077493f3487c8399e05
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522999"
---
# <a name="spinlockdprrelease-rule-ndis"></a>SpinLockDprRelease 规则 (ndis)


**SpinLockDprRelease**规则验证的调用[ **NdisAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff560699)或者[ **NdisDprAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff561749)仅当释放调节锁"解除锁定"状态时调用。 此规则还检查之前退出微型端口处理程序例程旋转锁都已被发布。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>SpinLockDprRelease</strong>规则。</p>
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

[**NdisAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff560699)
[**NdisAllocateSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff561617)
[**NdisDprAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff561749)
[**NdisDprReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff561753)
[**NdisReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff564524)
 

 





