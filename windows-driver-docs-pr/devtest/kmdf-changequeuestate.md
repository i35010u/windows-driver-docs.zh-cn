---
title: 'ChangeQueueState 规则 (kmdf) '
description: ChangeQueueState 规则指定 WDF 驱动程序不会尝试更改并发线程的队列状态，也不会从同一线程内的另一次调用状态更改 DDIs。
ms.assetid: C05A04E8-F8F2-4339-AAB7-FD62BE1DAAA2
ms.date: 05/21/2018
keywords:
- 'ChangeQueueState 规则 (kmdf) '
topic_type:
- apiref
api_name:
- ChangeQueueState
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ce1e7f1f4ddff294000fd251a11d1fc30eb5a732
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103350"
---
# <a name="changequeuestate-rule-kmdf"></a>ChangeQueueState 规则 (kmdf) 


**ChangeQueueState**规则指定 WDF 驱动程序不会尝试更改并发线程的队列状态，也不会从同一线程内的另一次调用状态更改 DDIs。 队列状态更改回调函数为 [**WdfIoQueueStop**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop)、 [**WdfIoQueueStopSynchronously**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopsynchronously)、[**WdfIoQueuePurge**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurge)、[**WdfIoQueuePurgeSynchronously**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurgesynchronously)、 [**WdfIoQueueDrain**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrain)、 [**WdfIoQueueDrainSynchronously**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)、 [**WdfIoQueueStopAndPurge**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurge) 和 [**WdfIoQueueStopAndPurgeSynchronously**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously)。 如果在队列状态更改已经正在进行时调用这些 DDIs，将导致计算机崩溃或停止响应。

**驱动程序模型： KMDF**

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>ChangeQueueState</strong> 规则。</p>
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

[**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 
[**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate) 
[**WdfIoQueueCreate**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate) 
[**WdfIoQueueDrain**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrain) 
[**WdfIoQueueDrainSynchronously**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrainsynchronously) 
[**WdfIoQueuePurge**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurge) 
[**WdfIoQueuePurgeSynchronously**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurgesynchronously) 
[**WdfIoQueueStop**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop) 
[**WdfIoQueueStopAndPurge**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurge) 
[**WdfIoQueueStopAndPurgeSynchronously**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously) 
[**WdfIoQueueStopSynchronously**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopsynchronously)
