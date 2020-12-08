---
title: 'IrqlExPassive 规则 (wdm) '
description: IrqlExPassive 规则指定驱动程序只调用以下执行程序支持例程，PASSIVE_LEVEL。 IrqlExPassive 规则还指定驱动程序以 IRQL APC_LEVEL 调用 ExRaiseStatus。
ms.date: 05/21/2018
keywords:
- 'IrqlExPassive 规则 (wdm) '
topic_type:
- apiref
api_name:
- IrqlExPassive
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cbd7a9714a2b1e9a37a5a79beba86c88b6301fda
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828105"
---
# <a name="irqlexpassive-rule-wdm"></a>IrqlExPassive 规则 (wdm) 


**IrqlExPassive** 规则指定驱动程序只调用以下执行程序支持例程 \_ ：

-   [**ExCreateCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback)

-   [**ExIsProcessorFeaturePresent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisprocessorfeaturepresent)

-   [**ExRaiseAccessViolation**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraiseaccessviolation)

-   [**ExRaiseDatatypeMisalignment**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraisedatatypemisalignment)

-   [**ExRaiseStatus**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exraisestatus)

-   [**ExUuidCreate**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exuuidcreate)

**IrqlExPassive** 规则还指定驱动程序调用 [**ExRaiseStatus**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exraisestatus)的 IRQL &lt; \_ 级别。

**驱动程序模型： WDM**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0X00020008) ， [**bug 检查0xA： IRQL \_ 不 \_ 小于 \_ 或 \_ 等于**](../debugger/bug-check-0xa--irql-not-less-or-equal.md)


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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IrqlExPassive</strong> 规则。</p>
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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 " <a href="/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](./ddi-compliance-checking.md)">DDI 相容性检查</a> " 选项。</p></td>
</tr>
</tbody>
</table>



<a name="applies-to"></a>适用于
----------

[**ExCreateCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback) 
[**ExIsProcessorFeaturePresent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisprocessorfeaturepresent) 
[**ExRaiseAccessViolation**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraiseaccessviolation) 
[**ExRaiseDatatypeMisalignment**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraisedatatypemisalignment) 
[**ExRaiseStatus**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exraisestatus) 
[**ExUuidCreate**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exuuidcreate)另请参阅
--------

[**管理硬件优先级**](../kernel/managing-hardware-priorities.md) 
[**使用自旋锁时防止错误和死锁**](../kernel/preventing-errors-and-deadlocks-while-using-spin-locks.md)
