---
title: MarkingQueuedIrps 规则 (wdm)
description: MarkingQueuedIrps 规则指定的驱动程序调用的 IRP 需要进一步处理仅在持有自旋锁。 此规则仅适用于该驱动程序将 IRP 添加到驱动程序管理的队列。
ms.assetid: 3a70ba52-c62f-4574-9a2e-4ba7aed82529
ms.date: 05/21/2018
keywords:
- MarkingQueuedIrps 规则 (wdm)
topic_type:
- apiref
api_name:
- MarkingQueuedIrps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 01f10ef35b097bb5acd9e7ec727db5ee2c1c3ece
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392036"
---
# <a name="markingqueuedirps-rule-wdm"></a>MarkingQueuedIrps 规则 (wdm)


**MarkingQueuedIrps**规则指定驱动程序调用[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)的 IRP 需要进一步处理仅在持有自旋锁。 此规则仅适用于该驱动程序将 IRP 添加到驱动程序管理的队列。

具体而言，该驱动程序与此规则的冲突时，才*所有*以下事件的发生。

-   驱动程序调用[ **KeAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)或[ **KeAcquireInStackQueuedSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))获取自旋锁。

-   该驱动程序调用以下例程将 IRP 添加到驱动程序管理队列之一：
    -   [**InsertHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-insertheadlist)
    -   [**InsertTailList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-inserttaillist)
    -   [**KeInsertDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertdevicequeue)
    -   [**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertqueuedpc)
    -   [**KeInsertByKeyDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertbykeydevicequeue)
-   驱动程序调用[ **KeReleaseSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)或[ **KeReleaseInStackQueuedSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock)调用之前释放自旋锁**IoMarkIrpPending**。

-   该驱动程序返回的状态\_IRP 的待决。

驱动程序应调用**IoMarkIrpPending**只能同时保留数值调节钮锁定排队 IRP 的。 否则为无法取消排队，另一个驱动程序例程，完成并释放通过对调用之前系统 IRP **IoMarkIrpPending**发生，从而会导致崩溃。

有关详细信息，请参阅[**同步 IRP 取消**](https://docs.microsoft.com/windows-hardware/drivers/kernel/synchronizing-irp-cancellation)。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>MarkingQueuedIrps</strong>规则。</p>
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

[**InsertHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-insertheadlist)
[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)
[**IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending) 
 [ **KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))
[**KeAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)
 [ **KeInsertByKeyDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertbykeydevicequeue)
[**KeInsertDeviceQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertdevicequeue) 
 [ **KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertqueuedpc)
[**KeReleaseInStackQueuedSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock) 
[ **KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)
[**PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) 
 [ **RemoveHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-removeheadlist)
 

 





