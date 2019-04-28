---
title: SpinLockSafe 规则 (storport)
description: 此规则验证的 IoStartNextPacket IoCompleteRequest 例程不会占用自旋锁时调用。
ms.assetid: 12D36178-C00D-44A7-9DA0-E0663DF1FFDC
ms.date: 05/21/2018
keywords:
- SpinLockSafe 规则 (storport)
topic_type:
- apiref
api_name:
- SpinLockSafe
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cd1ee8a5739e446b485d048e4fc7d50dc6045c42
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345775"
---
# <a name="spinlocksafe-rule-storport"></a>SpinLockSafe 规则 (storport)


此规则验证**IoStartNextPacket**并**IoCompleteRequest**例程不会占用自旋锁时调用。 规则跟踪的数值调节钮持有的锁数量在任何时候，如果该数字不是 0 时调用任一例程时，该驱动程序未能通过该规则。

|              |          |
|--------------|----------|
| 驱动程序模型 | Storport |

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

<a name="applies-to"></a>适用对象
----------

[**IoAcquireCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff548196)
[**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)
[**IoReleaseCancelSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff549550) 
 [ **IoStartNextPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550358)
[**KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)
 [ **KeAcquireSpinLockAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff551921)
[**KeReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145) 
 [ **KeReleaseSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553150)
 

 





