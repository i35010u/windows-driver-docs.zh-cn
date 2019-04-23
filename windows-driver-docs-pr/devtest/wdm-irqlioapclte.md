---
title: IrqlIoApcLte 规则 (wdm)
description: IrqlIoApcLte 规则指定驱动程序调用以下 I/O 管理器例程，仅当执行在 IRQL APC_LEVEL 时。
ms.assetid: 1f0b2b9c-f67c-4e34-b079-6a2769f62879
ms.date: 05/21/2018
keywords:
- IrqlIoApcLte 规则 (wdm)
topic_type:
- apiref
api_name:
- IrqlIoApcLte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8590ef02ee78e22a580449bfb0f2172d829008e5
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902871"
---
# <a name="irqlioapclte-rule-wdm"></a>IrqlIoApcLte 规则 (wdm)


**IrqlIoApcLte**规则指定驱动程序调用以下 I/O 管理器例程，仅当执行在 IRQL &lt;= APC\_级别：

-   [**IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)

-   [**IoGetInitialStack**](https://msdn.microsoft.com/library/windows/hardware/ff549247)

-   [**IoRaiseHardError**](https://msdn.microsoft.com/library/windows/hardware/ff549482)

-   [**IoRaiseInformationalHardError**](https://msdn.microsoft.com/library/windows/hardware/ff549488)

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

|                                   |                                                                                                                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00020009) [ **Bug 检查 0xA:IRQL\_不\_较少\_或\_相等**](https://msdn.microsoft.com/library/windows/hardware/ff560129) |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>IrqlIoApcLte</strong>规则。</p>
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

[**IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)
[**IoGetInitialStack**](https://msdn.microsoft.com/library/windows/hardware/ff549247)
[**IoRaiseHardError** ](https://msdn.microsoft.com/library/windows/hardware/ff549482)
 [ **IoRaiseInformationalHardError** ](https://msdn.microsoft.com/library/windows/hardware/ff549488)另请参阅
--------

[**管理硬件优先级**](https://msdn.microsoft.com/library/windows/hardware/ff554368)
[**使用自旋锁的同时防止错误和死锁**](https://msdn.microsoft.com/library/windows/hardware/ff559854)
 

 





