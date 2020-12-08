---
title: 'IrqlIoApcLte 规则 (wdm) '
description: IrqlIoApcLte 规则指定，仅当驱动程序以 IRQL APC_LEVEL 执行时，驱动程序才调用以下 i/o 管理器例程。
ms.date: 05/21/2018
keywords:
- 'IrqlIoApcLte 规则 (wdm) '
topic_type:
- apiref
api_name:
- IrqlIoApcLte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e30d3894b41903c5564012598c9cd6470ce89a8b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791893"
---
# <a name="irqlioapclte-rule-wdm"></a>IrqlIoApcLte 规则 (wdm) 


**IrqlIoApcLte** 规则指定，仅当驱动程序在 IRQL &lt; = APC 级别执行时，才调用以下 i/o 管理器例程 \_ ：

-   [**IoDeleteDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)

-   [**IoGetInitialStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetinitialstack)

-   [**IoRaiseHardError**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioraiseharderror)

-   [**IoRaiseInformationalHardError**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioraiseinformationalharderror)

**驱动程序模型： WDM**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0X00020009) ， [**bug 检查0xA： IRQL \_ 不 \_ 小于 \_ 或 \_ 等于**](../debugger/bug-check-0xa--irql-not-less-or-equal.md)


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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IrqlIoApcLte</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**IoDeleteDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice) 
[**IoGetInitialStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetinitialstack) 
[**IoRaiseHardError**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioraiseharderror) 
[**IoRaiseInformationalHardError**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioraiseinformationalharderror)另请参阅
--------

[**管理硬件优先级**](../kernel/managing-hardware-priorities.md) 
[**使用自旋锁时防止错误和死锁**](../kernel/preventing-errors-and-deadlocks-while-using-spin-locks.md)
