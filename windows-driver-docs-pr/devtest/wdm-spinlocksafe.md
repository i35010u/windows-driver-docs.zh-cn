---
title: SpinLockSafe 规则 (wdm)
description: SpinLockSafe 规则指定 IoStartNextPacket 和 IoCompleteRequest 不调用同时保留数值调节钮锁定。
ms.assetid: 64a18cb0-80a3-4830-a5b0-131fc1ebdf60
ms.date: 05/21/2018
keywords:
- SpinLockSafe 规则 (wdm)
topic_type:
- apiref
api_name:
- SpinLockSafe
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0c331eb451424e526b04538e4b6592be99944943
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546607"
---
# <a name="spinlocksafe-rule-wdm"></a>SpinLockSafe 规则 (wdm)


**SpinLockSafe**规则指定[ **IoStartNextPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550358)并[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)不占用自旋锁时调用。

此规则还指定驱动程序调用[ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)或[ **KeAcquireSpinLockAtDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff551921)调用前[**KeReleaseSpinLockFromDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff553150)或[ **KeReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553145)，和它调用[ **IoAcquireCancelSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff548196)之前，调用[ **IoReleaseCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff549550)。

如果该驱动程序包含嵌套的自旋锁，即使这些自旋锁获得和释放正确，static Driver Verifier 可报告 false 违反此规则。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>SpinLockSafe</strong>规则。</p>
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

[**IoAcquireCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff548196)
[**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)
[**IoReleaseCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff549550) 
 [ **IoStartNextPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550358)
[**KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)
 [ **KeAcquireSpinLockRaiseToDpc**](https://msdn.microsoft.com/library/windows/hardware/ff551928)
[**KeReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553145)
 

 





