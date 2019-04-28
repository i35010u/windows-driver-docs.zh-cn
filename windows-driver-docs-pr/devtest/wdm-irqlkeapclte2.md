---
title: IrqlKeApcLte2 规则 (wdm)
ms.assetid: 585d741d-543f-421b-be48-28f48d68fc4d
ms.date: 05/21/2018
description: ''
keywords:
- IrqlKeApcLte2 规则 (wdm)
topic_type:
- apiref
api_name:
- IrqlKeApcLte2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: de243d303667476b3831123a166fc3a94e39573b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341614"
---
# <a name="irqlkeapclte2-rule-wdm"></a>IrqlKeApcLte2 规则 (wdm)


**IrqlKeApcLte2**规则指定驱动程序调用以下内核例程，仅当执行在 IRQL &lt;= APC\_级别：

-   [**KeAreAllApcsDisabled**](https://msdn.microsoft.com/library/windows/hardware/ff551935)

-   [**KeAreApcsDisabled**](https://msdn.microsoft.com/library/windows/hardware/ff551938)

-   [**KeDeregisterNmiCallback**](https://msdn.microsoft.com/library/windows/hardware/ff552008)

-   [**KeEnterCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552021)

-   [**KeEnterGuardedRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552028)

-   [**KeLeaveCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552964)

-   [**KeLeaveGuardedRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552967)

-   [**KeRegisterNmiCallback**](https://msdn.microsoft.com/library/windows/hardware/ff553116)

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00020010) |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrqlKeApcLte2</strong>规则。</p>
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

[**KeDeregisterNmiCallback**](https://msdn.microsoft.com/library/windows/hardware/ff552008)
[**KeEnterCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552021)
[**KeEnterGuardedRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552028) 
 [ **KeLeaveCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552964)
[**KeLeaveGuardedRegion** ](https://msdn.microsoft.com/library/windows/hardware/ff552967) 
 [ **KeRegisterNmiCallback**](https://msdn.microsoft.com/library/windows/hardware/ff553116)
 

 





