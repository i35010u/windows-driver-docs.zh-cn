---
title: CompletionRoutineRegistered 规则（wdm）
description: CompletionRoutineRegistered 规则指定如果调度例程使用 IoSetCompletionRoutineEx 注册了 IoCompletion 例程，则调度例程之后必须调用 IoCallDriver 或 PoCallDriver。
ms.assetid: ee0d813c-3bcc-4688-902c-1a2d15ddfd09
ms.date: 05/21/2018
keywords:
- CompletionRoutineRegistered 规则（wdm）
topic_type:
- apiref
api_name:
- CompletionRoutineRegistered
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f941b7636ed3b8a8928a0109655e1be2e0a15667
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917831"
---
# <a name="completionroutineregistered-rule-wdm"></a>CompletionRoutineRegistered 规则（wdm）


**CompletionRoutineRegistered**规则指定如果调度例程使用[**IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)注册了[**IoCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，则调度例程之后必须调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)或[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)。

在**IoCompletion**例程执行之前， **IoSetCompletionRoutineEx**例程会分配保留分配的内存。 驱动程序必须确保**IoCompletion**例程通过调用**IoCallDriver**或**PoCallDriver**来执行;否则，内核将泄漏内存。

**驱动程序模型： WDM**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>CompletionRoutineRegistered</strong>规则。</p>
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

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 
[**IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex) 
[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)
 

 





