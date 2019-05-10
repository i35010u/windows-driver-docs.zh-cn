---
title: IrqlExApcLte2 规则 (wdm)
description: IrqlExApcLte2 规则指定驱动程序调用以下例程只能在 IRQL APC\_级别。
ms.assetid: 5800ec58-2084-4092-9614-dd631458c7dd
ms.date: 05/21/2018
keywords:
- IrqlExApcLte2 规则 (wdm)
topic_type:
- apiref
api_name:
- IrqlExApcLte2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a5f72e8bca9cbf4561779374b971470a48e1d238
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359443"
---
# <a name="irqlexapclte2-rule-wdm"></a>IrqlExApcLte2 规则 (wdm)


**IrqlExApcLte2**规则指定驱动程序只能在 IRQL 调用以下例程&lt;= APC\_级别。

-   [**CmRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff541918)

-   [**CmUnRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff541928)

-   [**ExAllocateFromPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544393)

-   [**ExAllocatePoolWithQuota**](https://msdn.microsoft.com/library/windows/hardware/ff544506)

-   [**ExAllocatePoolWithQuotaTag**](https://msdn.microsoft.com/library/windows/hardware/ff544513)

-   [**ExDeletePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544570)

-   [**ExFreeToPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544605)

-   [**ExInitializePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545309)

-   [**ExRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff545534)

-   [**ExSetTimerResolution**](https://msdn.microsoft.com/library/windows/hardware/ff545614)

-   [**ExUnregisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff545649)

-   [**ProbeForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559876)

-   [**ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

|                                   |                                                                                                                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00020006) [ **Bug 检查 0xA:IRQL\_不\_较少\_或\_相等**](https://msdn.microsoft.com/library/windows/hardware/ff560129) |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrqlExApcLte2</strong>规则。</p>
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

[**CmRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff541918)
[**CmRegisterCallbackEx**](https://msdn.microsoft.com/library/windows/hardware/ff541921)
[**CmUnRegisterCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff541928) 
 [ **ExDeletePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544570)
[**ExInitializePagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff545309) 
 [ **ExRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff545534)
[**ExSetTimerResolution** ](https://msdn.microsoft.com/library/windows/hardware/ff545614)
 [ **ExUnregisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff545649)
[**ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876) 
 [**ProbeForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff559879)
 

 





