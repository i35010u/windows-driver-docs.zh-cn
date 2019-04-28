---
title: MarkPowerDown 规则 (wdm)
description: MarkPowerDown 规则指定 IRP\_MJ\_IRP 功能\_MN\_设置\_的电源可用于从 s0 到 SystemPowerState IRP \ S1...S5\ 是挂起。
ms.assetid: 5C35F607-1550-4B48-8325-8A01D522786F
ms.date: 05/21/2018
keywords:
- MarkPowerDown 规则 (wdm)
topic_type:
- apiref
api_name:
- MarkPowerDown
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 12cf2994e8a1286ac68ce51c984ed83e40d22d33
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329727"
---
# <a name="markpowerdown-rule-wdm"></a>MarkPowerDown 规则 (wdm)


**MarkPowerDown**规则指定 IRP\_MJ\_与 IRP POWER\_MN\_设置\_用于电源**SystemPowerState** IRP从 s0 到\[S1...S5\]都会被挂起。

此规则仅适用于 FDO 和 FIDO 驱动程序。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>MarkPowerDown</strong>规则。</p>
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

[**IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)
[**IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)
[**IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)
 [ **IoGetDeviceInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff549186)
[**IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422) 
[ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)
[**IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679) 
[ **IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





