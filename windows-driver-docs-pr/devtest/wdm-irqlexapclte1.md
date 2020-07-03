---
title: IrqlExApcLte1 规则（wdm）
description: IrqlExApcLte1 规则指定驱动程序仅调用 ExAcquireFastMutex 和 ExTryToAcquireFastMutex，APC_LEVEL。
ms.assetid: c86aa593-03b5-4a65-9cef-3b64fcc3d5fd
ms.date: 05/21/2018
keywords:
- IrqlExApcLte1 规则（wdm）
topic_type:
- apiref
api_name:
- IrqlExApcLte1
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0ca13fe2b33fb2648e8152ad44211e2debd41b04
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916842"
---
# <a name="irqlexapclte1-rule-wdm"></a>IrqlExApcLte1 规则（wdm）


**IrqlExApcLte1**规则指定驱动程序只调用[**ExAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))和[**ExTryToAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85)) ，而不是以 IRQL &lt; = APC \_ 级别。

**驱动程序模型： WDM**

|                                   |                                                                                                                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 找到了具有此规则的 Bug 检查 | [**Bug 检查0xC4：驱动程序 \_验证器 \_ 检测到 \_ 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0X00020005）， [ **Bug 检查0xA： IRQL \_ 不 \_ 小于 \_ 或 \_ 等于**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xa--irql-not-less-or-equal) |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>IrqlExApcLte1</strong>规则。</p>
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

[**ExAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85)) 
[**ExTryToAcquireFastMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85))另请参阅
--------

[**管理硬件优先级**](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-hardware-priorities) 
[**使用自旋锁时防止错误和死锁**](https://docs.microsoft.com/windows-hardware/drivers/kernel/preventing-errors-and-deadlocks-while-using-spin-locks)
 

 





