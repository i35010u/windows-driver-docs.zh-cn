---
title: IrqlIoApcLte 规则（wdm）
description: IrqlIoApcLte 规则指定，仅当驱动程序以 IRQL APC_LEVEL 执行时，驱动程序才调用以下 i/o 管理器例程。
ms.assetid: 1f0b2b9c-f67c-4e34-b079-6a2769f62879
ms.date: 05/21/2018
keywords:
- IrqlIoApcLte 规则（wdm）
topic_type:
- apiref
api_name:
- IrqlIoApcLte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 771321e9b9c765ae9e17661bd2c24dc4be0dcfb5
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916196"
---
# <a name="irqlioapclte-rule-wdm"></a>IrqlIoApcLte 规则（wdm）


**IrqlIoApcLte**规则指定，仅当驱动程序在 IRQL &lt; = APC 级别执行时，才调用以下 i/o 管理器例程 \_ ：

-   [**IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)

-   [**IoGetInitialStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetinitialstack)

-   [**IoRaiseHardError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioraiseharderror)

-   [**IoRaiseInformationalHardError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioraiseinformationalharderror)

**驱动程序模型： WDM**

|                                   |                                                                                                                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 找到了具有此规则的 Bug 检查 | [**Bug 检查0xC4：驱动程序 \_验证器 \_ 检测到 \_ 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0X00020009）， [ **Bug 检查0xA： IRQL \_ 不 \_ 小于 \_ 或 \_ 等于**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xa--irql-not-less-or-equal) |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>IrqlIoApcLte</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**IoDeleteDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice) 
[**IoGetInitialStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetinitialstack) 
[**IoRaiseHardError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioraiseharderror) 
[**IoRaiseInformationalHardError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioraiseinformationalharderror)另请参阅
--------

[**管理硬件优先级**](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-hardware-priorities) 
[**使用自旋锁时防止错误和死锁**](https://docs.microsoft.com/windows-hardware/drivers/kernel/preventing-errors-and-deadlocks-while-using-spin-locks)
 

 





