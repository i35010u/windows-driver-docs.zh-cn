---
title: IrqlKeDispatchLte 规则 (wdm)
ms.assetid: 425a20ea-c9e3-45f4-a517-6bad9ab0de98
ms.date: 05/21/2018
description: ''
keywords:
- IrqlKeDispatchLte 规则 (wdm)
topic_type:
- apiref
api_name:
- IrqlKeDispatchLte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 22fe0d717046da2ab5a33b6c1338eff6396565df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577519"
---
# <a name="irqlkedispatchlte-rule-wdm"></a>IrqlKeDispatchLte 规则 (wdm)


**IrqlKeDispatchLte**规则指定驱动程序调用以下内核例程，仅当执行在 IRQL &lt;= 调度\_级别：

-   [**KeAcquireSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff551917)

-   [**KeCancelTimer**](https://msdn.microsoft.com/library/windows/hardware/ff551970)

-   [**KeClearEvent**](https://msdn.microsoft.com/library/windows/hardware/ff551980)

-   [**KeFlushIoBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff552041)

-   [**KeInitializeDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff552126)

-   [**KeInitializeTimer**](https://msdn.microsoft.com/library/windows/hardware/ff552168)

-   [**KeInitializeTimerEx**](https://msdn.microsoft.com/library/windows/hardware/ff552173)

-   [**KePulseEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552979)

-   [**KeRaiseIrqlToDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553084)

-   [**KeReadStateEvent**](https://msdn.microsoft.com/library/windows/hardware/ff553089)

-   [**KeReadStateTimer**](https://msdn.microsoft.com/library/windows/hardware/ff553099)

-   [**KeReleaseMutex**](https://msdn.microsoft.com/library/windows/hardware/ff553140)

-   [**KeRemoveEntryDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff553163)

-   [**KeResetEvent**](https://msdn.microsoft.com/library/windows/hardware/ff553176)

-   [**KeSaveFloatingPointState**](https://msdn.microsoft.com/library/windows/hardware/ff553243)

-   [**KeSetTimer**](https://msdn.microsoft.com/library/windows/hardware/ff553286)

-   [**KeSetTimerEx**](https://msdn.microsoft.com/library/windows/hardware/ff553292)

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00020011) |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrqlKeDispatchLte</strong>规则。</p>
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
[**KeCancelTimer**](https://msdn.microsoft.com/library/windows/hardware/ff551970)
[**KeClearEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff551980) 
 [ **KeInitializeDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff552126)
[**KeInitializeSemaphore** ](https://msdn.microsoft.com/library/windows/hardware/ff552150) 
[ **KeInitializeTimer**](https://msdn.microsoft.com/library/windows/hardware/ff552168)
[**KeInitializeTimerEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552173) 
 [**KePulseEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552979)
[**KeReadStateEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff553089) 
 [ **KeReadStateTimer**](https://msdn.microsoft.com/library/windows/hardware/ff553099)
[**KeReleaseMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff553140) 
 [ **KeRemoveEntryDeviceQueue**](https://msdn.microsoft.com/library/windows/hardware/ff553163)
[**KeResetEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff553176) 
 [ **KeSaveFloatingPointState**](https://msdn.microsoft.com/library/windows/hardware/ff553243)
[**KeSetTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff553286) 
 [ **KeSetTimerEx**](https://msdn.microsoft.com/library/windows/hardware/ff553292)
 

 





