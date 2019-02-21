---
title: IrqlKeApcLte1 规则 (wdm)
ms.assetid: d88e3c0f-574b-41df-97ee-282a9f1eb6f4
ms.date: 05/21/2018
description: ''
keywords:
- IrqlKeApcLte1 规则 (wdm)
topic_type:
- apiref
api_name:
- IrqlKeApcLte1
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 93a099231f27e801c1c15f0ea4b41461520ac551
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525663"
---
# <a name="irqlkeapclte1-rule-wdm"></a>IrqlKeApcLte1 规则 (wdm)


**IrqlKeApcLte1**规则指定驱动程序调用以下内核例程，仅当执行在 IRQL &lt;= APC\_级别：

-   [**KeAcquireGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff551892)

-   [**KeAcquireGuardedMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff551894)

-   [**KeDelayExecutionThread**](https://msdn.microsoft.com/library/windows/hardware/ff551986)

-   [**KeQueryActiveProcessors**](https://msdn.microsoft.com/library/windows/hardware/ff553001)

-   [**KeReleaseGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff553124)

-   [**KeReleaseGuardedMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff553125)

-   [**KeTryToAcquireGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff553307)

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x0002000F) |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrqlKeApcLte1</strong>规则。</p>
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

 

<a name="applies-to"></a>适用于
----------

[**KeAcquireGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff551892)
[**KeAcquireGuardedMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff551894)
[**KeDelayExecutionThread** ](https://msdn.microsoft.com/library/windows/hardware/ff551986) 
 [ **KeQueryActiveProcessors**](https://msdn.microsoft.com/library/windows/hardware/ff553001)
[**KeReleaseGuardedMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff553124) 
 [ **KeReleaseGuardedMutexUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff553125)
[**KeTryToAcquireGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff553307)
 

 





