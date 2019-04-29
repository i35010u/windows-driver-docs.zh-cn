---
title: StartIoCancel 规则 (wdm)
description: StartIoCancel 规则指定，该驱动程序必须不调用 IoSetStartIoAttributes 并无法参数设置为 FALSE 与非 NULLCancel 例程调用 IoSetCancelRoutine 之前。
ms.assetid: 08fde0b1-4f4e-473a-9e07-3b39683a3a1b
ms.date: 05/21/2018
keywords:
- StartIoCancel 规则 (wdm)
topic_type:
- apiref
api_name:
- StartIoCancel
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9104f7a70dfc40e779cec24eabef8e7f0451016c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380443"
---
# <a name="startiocancel-rule-wdm"></a>StartIoCancel 规则 (wdm)


**StartIoCancel**规则指定驱动程序必须调用[ **IoSetStartIoAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff550330)与*无法*参数设置为**FALSE**之前，调用[ **IoSetCancelRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549674)与非**NULL** [ **取消**](https://msdn.microsoft.com/library/windows/hardware/ff540742)例程。

设置*无法*参数**FALSE**在注册之前[**取消**](https://msdn.microsoft.com/library/windows/hardware/ff540742)例程可能会导致取消争用条件。

因为驱动程序的[**取消**](https://msdn.microsoft.com/library/windows/hardware/ff540742)例程必须包括对[ **IoReleaseCancelSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549550) (若要释放数值调节钮锁定的 I/O管理器之前，先将获取**取消**例程)，验证两个驱动程序，请考虑**StartIoCancel**规则并[ **CancelSpinLock** ](wdm-cancelspinlock.md)规则。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>StartIoCancel</strong>规则。</p>
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

[**IoSetCancelRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549674)
[**IoSetStartIoAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff550330)另请参阅
--------

[**CancelSpinLock**](wdm-cancelspinlock.md)
 

 





