---
title: MarkPower 规则 (wdm)
description: MarkPower 规则指定 IRP\_MJ\_IRP 功能\_MN\_设置\_都会被挂起，转到 S0 SystemPowerState IRP 的电源。 此规则仅适用于 FDO 和 FIDO 驱动程序。
ms.assetid: 2EF5F14B-F474-4583-B7AC-70142BC3D831
ms.date: 05/21/2018
keywords:
- MarkPower 规则 (wdm)
topic_type:
- apiref
api_name:
- MarkPower
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 854490c64c4e90d47d45d3f231501dae6d28fe5b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554709"
---
# <a name="markpower-rule-wdm"></a>MarkPower 规则 (wdm)


**MarkPower**规则指定 IRP\_MJ\_与 IRP POWER\_MN\_设置\_用于电源**SystemPowerState** IRP 转到S0 是挂起。 此规则仅适用于 FDO 和 FIDO 驱动程序。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>MarkPower</strong>规则。</p>
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

[**IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)
[**IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)
[**IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)
 [ **IoGetDeviceInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff549186)
[**IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422) 
[ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)
[**IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679) 
[ **IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





