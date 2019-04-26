---
title: IrqlMmApcLte 规则 (wdm)
ms.assetid: 075f5710-b2bf-4546-9648-661a3c8521f8
ms.date: 05/21/2018
description: ''
keywords:
- IrqlMmApcLte 规则 (wdm)
topic_type:
- apiref
api_name:
- IrqlMmApcLte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cb212f8a9b4f230641de54ddb3fe703a5d756efa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331373"
---
# <a name="irqlmmapclte-rule-wdm"></a>IrqlMmApcLte 规则 (wdm)


**IrqlMmApcLte**规则指定，该驱动程序调用以下内存管理器例程仅当执行在 IRQL &lt;= APC\_级别：

-   [**MmAllocateNonCachedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554479)

-   [**MmFreeNonCachedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554516)

-   [**MmAllocatePagesForMdl**](https://msdn.microsoft.com/library/windows/hardware/ff554482)

-   [**MmFreePagesFromMdl**](https://msdn.microsoft.com/library/windows/hardware/ff554521)

-   [**MmLockPagableDataSection**](https://msdn.microsoft.com/library/windows/hardware/ff554607)

-   [**MmLockPagableSectionByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff554610)

-   [**MmPageEntireDriver**](https://msdn.microsoft.com/library/windows/hardware/ff554650)

-   [**MmResetDriverPaging**](https://msdn.microsoft.com/library/windows/hardware/ff554680)

-   [**MmSecureVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff556374)

-   [**MmUnlockPagableImageSection**](https://msdn.microsoft.com/library/windows/hardware/ff556377)

-   [**MmUnsecureVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff556395)

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00020019) |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrqlMmApcLte</strong>规则。</p>
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

[**MmAllocateNonCachedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554479)
[**MmAllocatePagesForMdl**](https://msdn.microsoft.com/library/windows/hardware/ff554482)
[**MmAllocatePagesForMdlEx** ](https://msdn.microsoft.com/library/windows/hardware/ff554489) 
 [ **MmFreeNonCachedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554516)
[**MmFreePagesFromMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff554521) 
 [ **MmLockPagableDataSection**](https://msdn.microsoft.com/library/windows/hardware/ff554607)
[**MmLockPagableSectionByHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff554610) 
 [ **MmPageEntireDriver**](https://msdn.microsoft.com/library/windows/hardware/ff554650)
[**MmResetDriverPaging** ](https://msdn.microsoft.com/library/windows/hardware/ff554680) 
 [ **MmSecureVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff556374)
[**MmUnlockPagableImageSection** ](https://msdn.microsoft.com/library/windows/hardware/ff556377) 
 [ **MmUnsecureVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff556395)
 

 





