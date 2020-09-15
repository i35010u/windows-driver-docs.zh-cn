---
title: 'MarkingQueuedIrps 规则 (wdm) '
description: MarkingQueuedIrps 规则指定，驱动程序为 IRP 调用也，该 IRP 需要在持有自旋锁的情况下进行进一步处理。 仅当驱动程序将 IRP 添加到驱动程序管理的队列时，此规则才适用。
ms.assetid: 3a70ba52-c62f-4574-9a2e-4ba7aed82529
ms.date: 05/21/2018
keywords:
- 'MarkingQueuedIrps 规则 (wdm) '
topic_type:
- apiref
api_name:
- MarkingQueuedIrps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 14df28d0a9ffce120d9bf98fdd5b8b481b6d7130
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103476"
---
# <a name="markingqueuedirps-rule-wdm"></a>MarkingQueuedIrps 规则 (wdm) 


**MarkingQueuedIrps**规则指定，驱动程序为 IRP 调用[**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)，该 IRP 需要在持有自旋锁的情况下进行进一步处理。 仅当驱动程序将 IRP 添加到驱动程序管理的队列时，此规则才适用。

具体而言，只有在发生以下 *所有* 事件时，驱动程序才会违反此规则。

-   驱动程序调用 [**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 或 [**KeAcquireInStackQueuedSpinLock**](/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)) 以获取旋转锁。

-   驱动程序调用以下例程之一将 IRP 添加到驱动程序管理的队列：
    -   [**InsertHeadList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-insertheadlist)
    -   [**InsertTailList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-inserttaillist)
    -   [**KeInsertDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertdevicequeue)
    -   [**KeInsertQueueDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)
    -   [**KeInsertByKeyDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertbykeydevicequeue)
-   驱动程序调用 [**KeReleaseSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock) 或 [**KeReleaseInStackQueuedSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock) 以释放旋转锁，然后再调用 **也**。

-   驱动程序为 IRP 返回状态 \_ "正在挂起"。

只有持有自旋锁时，驱动程序才应为排队的 IRP 调用 **也** 。 否则，IRP 可以取消排队，由其他驱动程序例程完成，并在调用 **也** 之前由系统释放，从而导致崩溃。

有关详细信息，请参阅 [**同步 IRP 取消**](../kernel/synchronizing-irp-cancellation.md)。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>MarkingQueuedIrps</strong> 规则。</p>
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

[**InsertHeadList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-insertheadlist) 
[**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 
[**KeAcquireInStackQueuedSpinLock**](/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)) 
[**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 
[**KeInsertByKeyDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertbykeydevicequeue) 
[**KeInsertDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertdevicequeue) 
[**KeInsertQueueDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc) 
[**KeReleaseInStackQueuedSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock) 
[**KeReleaseSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock) 
[**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) 
[**RemoveHeadList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-removeheadlist)
