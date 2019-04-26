---
title: IoSetCompletionRoutineExCheck 规则 (wdm)
description: IoSetCompletionRoutineExCheck 规则指定 IoSetCompletionRoutineEx 例程返回 NTSTATUS 值。
ms.assetid: 047298DB-851A-4406-AD6D-5A276960ABE4
ms.date: 05/21/2018
keywords:
- IoSetCompletionRoutineExCheck 规则 (wdm)
topic_type:
- apiref
api_name:
- IoSetCompletionRoutineExCheck
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f716ff2a6804a1a7f62bb531c18106d4ad0b2368
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325327"
---
# <a name="iosetcompletionroutineexcheck-rule-wdm"></a>IoSetCompletionRoutineExCheck 规则 (wdm)


**IoSetCompletionRoutineExCheck**规则指定[ **IoSetCompletionRoutineEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549686)例程将返回 NTSTATUS 值。 该驱动程序必须检查此值可确定是否[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程已成功注册，然后再调[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)或[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)。

如果[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程成功注册[ **IoSetCompletionRoutineEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549686)分配保留的内存直到分配*IoCompletion*例程执行。 驱动程序必须确保他们*IoCompletion*例程通过调用执行[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)或者[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)否则，内核会发生内存泄漏。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IoSetCompletionRoutineExCheck</strong>规则。</p>
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

[**IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





