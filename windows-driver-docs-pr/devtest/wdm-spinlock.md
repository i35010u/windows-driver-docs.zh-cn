---
title: 旋转锁规则 (wdm)
description: 旋转锁规则指定，调用后 KeAcquireSpinLock，驱动程序会调用 KeReleaseSpinLock 之前 KeAcquireSpinLock 或 KeAcquireSpinLockRaiseToDpc 的后续调用。
ms.assetid: 3add467d-72b9-439f-b9a3-68f3d1e5b772
ms.date: 05/21/2018
keywords:
- 旋转锁规则 (wdm)
topic_type:
- apiref
api_name:
- SpinLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e04d5eef329968205ca9ba732cd7b1406824537d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327345"
---
# <a name="spinlock-rule-wdm"></a>旋转锁规则 (wdm)


**SpinLock**规则指定的在调用[ **KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)，驱动程序调用[ **KeReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553145)之前对后续调用**KeAcquireSpinLock**或设置为[ **KeAcquireSpinLockRaiseToDpc**](https://msdn.microsoft.com/library/windows/hardware/ff551928)。

如果它们是获取和释放锁不同资源的，允许嵌套的调用。 获取或释放的相同资源的锁嵌套的调用违反此规则。

此规则还指定驱动程序已使用[ **KeReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145)解除调度例程之前的所有数值调节钮锁定或取消例程结束。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00040009) |

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

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a> ，然后选择<a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[DDI compliance checking](https://msdn.microsoft.com/library/windows/hardware/hh454208)">DDI 符合性检查</a>选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用对象
----------

[**KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)
[**KeAcquireSpinLockRaiseToDpc**](https://msdn.microsoft.com/library/windows/hardware/ff551928)
[**KeReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553145)
[**KeTryToAcquireSpinLockAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553317)
 

 





