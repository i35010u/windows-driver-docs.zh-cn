---
title: EvtSurpriseRemoveNoSuspendQueue 规则（kmdf）
description: EvtSurpriseRemoveNoSuspendQueue 规则指定 WDF 驱动程序不应使用 EvtDeviceSurpriseRemoval 回调函数排出、停止或清除队列，而应使用自托管 i/o 回调函数。
ms.assetid: A22CC69F-AC48-4E2A-BE7E-9272810CB171
ms.date: 05/21/2018
keywords:
- EvtSurpriseRemoveNoSuspendQueue 规则（kmdf）
topic_type:
- apiref
api_name:
- EvtSurpriseRemoveNoSuspendQueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e78b81dba1f0ad39b53c2054f6f644ca0e17f174
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917091"
---
# <a name="evtsurpriseremovenosuspendqueue-rule-kmdf"></a>EvtSurpriseRemoveNoSuspendQueue 规则（kmdf）


**EvtSurpriseRemoveNoSuspendQueue**规则指定 WDF 驱动程序不应使用[*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)回调函数排出、停止或清除队列，而应使用自托管 i/o 回调函数。 *EvtDeviceSurpriseRemoval*回调函数未与电源线路径同步。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>EvtSurpriseRemoveNoSuspendQueue</strong>规则。</p>
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

[**WdfIoQueueDrain**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrain) 
[**WdfIoQueueDrainSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrainsynchronously) 
[**WdfIoQueuePurge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurge) 
[**WdfIoQueuePurgeSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurgesynchronously) 
[**WdfIoQueueStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop) 
[**WdfIoQueueStopAndPurge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurge) 
[**WdfIoQueueStopAndPurgeSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously) 
[**WdfIoQueueStopSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopsynchronously)
 

 





