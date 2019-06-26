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
ms.openlocfilehash: 8972a5ad364e5e17d6cac8c0f95188bb5e8e854d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393895"
---
# <a name="irqlioapclte-rule-wdm"></a>IrqlIoApcLte 规则 (wdm)


**IrqlIoApcLte**规则指定驱动程序调用以下 I/O 管理器例程，仅当执行在 IRQL &lt;= APC\_级别：

-   [**IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)

-   [**IoGetInitialStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetinitialstack)

-   [**IoRaiseHardError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioraiseharderror)

-   [**IoRaiseInformationalHardError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioraiseinformationalharderror)

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

|                                   |                                                                                                                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00020009) [ **Bug 检查 0xA:IRQL\_不\_较少\_或\_相等**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xa--irql-not-less-or-equal) |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>IrqlIoApcLte</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)
[**IoGetInitialStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetinitialstack)
[**IoRaiseHardError** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioraiseharderror)
 [ **IoRaiseInformationalHardError** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioraiseinformationalharderror)另请参阅
--------

[**管理硬件优先级**](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-hardware-priorities)
[**使用自旋锁的同时防止错误和死锁**](https://docs.microsoft.com/windows-hardware/drivers/kernel/preventing-errors-and-deadlocks-while-using-spin-locks)
 

 





