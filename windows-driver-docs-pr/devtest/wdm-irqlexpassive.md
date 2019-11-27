---
title: IrqlExPassive 规则（wdm）
description: IrqlExPassive 规则指定驱动程序只调用以下执行程序支持例程，PASSIVE_LEVEL。 IrqlExPassive 规则还指定驱动程序以 IRQL APC_LEVEL 调用 ExRaiseStatus。
ms.assetid: 92d73bd9-ce79-4be8-9ea2-a5aef2ea6edb
ms.date: 05/21/2018
keywords:
- IrqlExPassive 规则（wdm）
topic_type:
- apiref
api_name:
- IrqlExPassive
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 123c284c1e5fb50cdce025cdfadf21956032715e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839930"
---
# <a name="irqlexpassive-rule-wdm"></a>IrqlExPassive 规则（wdm）


**IrqlExPassive**规则指定驱动程序只调用以下执行程序支持例程： IRQL = 被动\_级别：

-   [**ExCreateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback)

-   [**ExIsProcessorFeaturePresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisprocessorfeaturepresent)

-   [**ExRaiseAccessViolation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraiseaccessviolation)

-   [**ExRaiseDatatypeMisalignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraisedatatypemisalignment)

-   [**ExRaiseStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exraisestatus)

-   [**ExUuidCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exuuidcreate)

**IrqlExPassive**规则还指定驱动程序以 IRQL &lt;= APC\_级别调用[**ExRaiseStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exraisestatus) 。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

|                                   |                                                                                                                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查0xC4：检测到\_冲突（0x00020008）的驱动程序\_验证程序\_** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) ， [ **BUG 检查0XA： IRQL\_没有\_或\_相等**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xa--irql-not-less-or-equal)\_ |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>IrqlExPassive</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">驱动程序验证程序</a>，并选择 " <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 相容性检查</a>" 选项。</p></td>
</tr>
</tbody>
</table>



<a name="applies-to"></a>适用于
----------

[**ExCreateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback)
[**ExIsProcessorFeaturePresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisprocessorfeaturepresent)
[**ExRaiseAccessViolation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraiseaccessviolation)
[**ExRaiseDatatypeMisalignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraisedatatypemisalignment)
[**ExRaiseStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exraisestatus)
[**ExUuidCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exuuidcreate)又
--------

[](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-hardware-priorities) [**在使用自旋锁时管理硬件优先级
防止错误和死锁**](https://docs.microsoft.com/windows-hardware/drivers/kernel/preventing-errors-and-deadlocks-while-using-spin-locks)








