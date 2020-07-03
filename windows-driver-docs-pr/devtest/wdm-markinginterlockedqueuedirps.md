---
title: MarkingInterlockedQueuedIrps 规则（wdm）
description: MarkingInterlockedQueuedIrps 规则指定，驱动程序将 IRP 正确地标记为 "挂起"，然后将其以联锁方式排队以进行进一步处理。
ms.assetid: a065b28f-f02a-45af-b9d9-754a36519b99
ms.date: 05/21/2018
keywords:
- MarkingInterlockedQueuedIrps 规则（wdm）
topic_type:
- apiref
api_name:
- MarkingInterlockedQueuedIrps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c5038c09e3e54aef9942c34e4264f53159e93c3f
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916245"
---
# <a name="markinginterlockedqueuedirps-rule-wdm"></a>MarkingInterlockedQueuedIrps 规则（wdm）


**MarkingInterlockedQueuedIrps**规则指定，驱动程序将 IRP 正确地标记为 "挂起"，然后将其以联锁方式排队以进行进一步处理。

此规则还指定驱动程序调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)，并将 irp 正确地标记为 "挂起"，然后调用以下任何函数将 irp 添加到联锁队列：

-   [**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397)

-   [**ExInterlockedInsertTailList**](https://msdn.microsoft.com/library/windows/hardware/ff545402)

-   [**ExInterlockedPushEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545418)

驱动程序应在添加 IRP 之前调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)，以要求更多地处理联锁队列。 否则，IRP 可以取消排队，由其他驱动程序例程完成，并在调用**也**之前由系统释放，从而导致崩溃。

有关详细信息，请参阅[**同步 IRP 取消**](https://docs.microsoft.com/windows-hardware/drivers/kernel/synchronizing-irp-cancellation)。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>MarkingInterlockedQueuedIrps</strong>规则。</p>
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

[**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397) 
[**ExInterlockedInsertTailList**](https://msdn.microsoft.com/library/windows/hardware/ff545402) 
[**ExInterlockedPushEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545418) 
[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 
[**RemoveHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-removeheadlist)另请参阅
--------

[**MarkIrpPending**](wdm-markirppending.md) 
[**正在同步 IRP 取消**](https://docs.microsoft.com/windows-hardware/drivers/kernel/synchronizing-irp-cancellation)
 

 





