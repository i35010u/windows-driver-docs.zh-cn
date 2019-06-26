---
title: CompleteRequestStatusCheck 规则 (wdm)
description: CompleteRequestStatusCheck 规则验证在 IRP 的 I/O 状态值匹配较低的驱动程序返回的状态值。
ms.assetid: 3B61137E-1D10-443B-A653-B32D638B17DB
ms.date: 05/21/2018
keywords:
- CompleteRequestStatusCheck 规则 (wdm)
topic_type:
- apiref
api_name:
- CompleteRequestStatusCheck
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6b6e8196c6515c72755c00dd028aaa7b7e3724f6
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393997"
---
# <a name="completerequeststatuscheck-rule-wdm"></a>CompleteRequestStatusCheck 规则 (wdm)


**CompleteRequestStatusCheck**规则验证是否在 IRP 的 I/O 状态值匹配较低的驱动程序返回的状态值。

如果 IRP 状态是状态，驱动程序的调度例程不应完成 IRP\_PENDING。

驱动程序的调度例程不应完成状态 IRP\_如果较低的驱动程序失败 IRP 的成功。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>CompleteRequestStatusCheck</strong>规则。</p>
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

[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioacquireremovelock)
[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)
[**IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)
 [ **IoMarkIrpPending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)
[**IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine) 
[ **IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex)
[**KeWaitForSingleObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject) 
 [**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)
 

 





