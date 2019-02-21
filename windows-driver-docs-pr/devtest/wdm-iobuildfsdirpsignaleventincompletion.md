---
title: IoBuildFsdIrpSignalEventInCompletion 规则
description: IoBuildFsdIrpSignalEventInCompletion 规则指定驱动程序，应在完成例程中调用 KeSetEvent Irp-PendingReturned 标志设置和完成例程处理本地创建异步 IRP 时。
ms.assetid: EBD84765-B517-447B-A6EF-0966054E7131
ms.date: 05/21/2018
keywords:
- IoBuildFsdIrpSignalEventInCompletion 规则
topic_type:
- apiref
api_name:
- IoBuildFsdIrpSignalEventInCompletion
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 64afe61f7d29ebe8f8920e065afdbe5762ce7b44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540803"
---
# <a name="iobuildfsdirpsignaleventincompletion-rule"></a>IoBuildFsdIrpSignalEventInCompletion 规则


**IoBuildFsdIrpSignalEventInCompletion**规则指定驱动程序应调用[ **KeSetEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff553253)中完成例程时**Irp-&gt;PendingReturned**设置标志，并开始处理本地创建异步 IRP 完成例程。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IoBuildFsdIrpSignalEventInCompletion</strong>规则。</p>
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

[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)
[**IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**KeInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552137)
[**KeSetEvent**](https://msdn.microsoft.com/library/windows/hardware/ff553253)
 

 





