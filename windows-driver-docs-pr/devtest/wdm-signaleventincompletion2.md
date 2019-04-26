---
title: SignalEventInCompletion2 规则 (wdm)
description: SignalEventInCompletion2 规则指定在处理异步 IRP，驱动程序需要时要调用 KeSetEvent 中完成例程 Irp-PendingReturned 标志设置。
ms.assetid: 48BFBB4D-0D42-4C83-8EA8-6874F31238FC
ms.date: 05/21/2018
keywords:
- SignalEventInCompletion2 规则 (wdm)
topic_type:
- apiref
api_name:
- SignalEventInCompletion2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2ef8d4af15a6ca3cbf6ea51fd3851f2b6bf3fe70
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325063"
---
# <a name="signaleventincompletion2-rule-wdm"></a>SignalEventInCompletion2 规则 (wdm)


**SignalEventInCompletion2**规则指定在处理异步 IRP，该驱动程序必须调用[ **KeSetEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff553253)中完成例程时**Irp-&gt;PendingReturned**设置标志。

在这种情况下，不会调用完成例程。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>SignalEventInCompletion2</strong>规则。</p>
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

[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)
[**IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**KeInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552137)
 

 





