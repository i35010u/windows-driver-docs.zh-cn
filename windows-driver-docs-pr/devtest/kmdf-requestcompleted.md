---
title: RequestCompleted 规则 (kmdf)
description: DeferredRequestCompleted 规则指定，对于非筛选器驱动程序提供给驱动程序的默认 I/O 队列的每个请求必须完成，除非请求延迟或转发，或如果调用 WdfRequestStopAcknowledge。
ms.assetid: fb034d81-d49d-43a5-92b9-9b4e3f3056ee
ms.date: 05/21/2018
keywords:
- RequestCompleted 规则 (kmdf)
topic_type:
- apiref
api_name:
- RequestCompleted
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bde1694a32be1f418a9c69237fafdd2df5cb310d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392911"
---
# <a name="requestcompleted-rule-kmdf"></a>RequestCompleted 规则 (kmdf)


[ **DeferredRequestCompleted** ](kmdf-deferredrequestcompleted.md)规则指定，对于非筛选器驱动程序提供给驱动程序的默认 I/O 队列的每个请求必须完成，除非请求延迟或转发，或如果[ **WdfRequestStopAcknowledge** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)调用。

在退出之前从 I/O 请求回调函数，除在以下情况下，必须完成 I/O 请求提供给驱动程序的默认队列通过队列回调函数之一：

-   请求已延迟 (到 DPC 或工作项，例如)。 在这种情况下，可以使用[DeferredRequestCompleted](kmdf-deferredrequestcompleted.md)规则。

-   请求已转发到 I/O 目标或另一个队列

-   请求已传递到框架 (通过调用[ **WdfDeviceEnqueueRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest))

-   [**WdfRequestStopAcknowledge** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)调用

从以下的回调函数的驱动程序退出时验证规则：

-   [*EvtIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)， [ *EvtCleanupCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)或者[ *EvtDestroyCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)队列

-   [*EvtCleanupCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)或[ *EvtDestroyCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)文件对象

-   [*EvtFileClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_file_close)， [ *EvtFileCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup)， [ *EvtDeviceSelfManagedIoSuspend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_suspend)， [ *EvtDeviceSelfManagedIoFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)， [ *EvtDeviceSelfManagedIoCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_cleanup)， [ *EvtDeviceShutdownNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfcontrol/nc-wdfcontrol-evt_wdf_device_shutdown_notification)， [ *EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)， [ *EvtCleanupCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)或[ *EvtDestroyCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)设备

-   [*EvtDriverUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)

请求演示文稿的 I/O 队列回调函数是[ *EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)， [ *EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)， [ *EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)， [ *EvtIoDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)，并[ *EvtIoInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)

|              |      |
|--------------|------|
| 驱动程序模型 | KMDF |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>RequestCompleted</strong>规则。</p>
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

[**WdfDeviceEnqueueRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)
[**WdfDmaTransactionInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize) 
 [ **WdfDmaTransactionInitializeUsingRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingrequest)
[**WdfIoTargetSendInternalIoctlOthersSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously) 
[ **WdfIoTargetSendInternalIoctlSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously)
[**WdfIoTargetSendIoctlSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously) 
 [ **WdfIoTargetSendReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)
[**WdfIoTargetSendWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously) 
 [ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)
[**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation) 
 [ **WdfRequestCompleteWithPriorityBoost** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) 
 [ **WdfRequestForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)
[**WdfRequestMarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable) 
 [ **WdfRequestMarkCancelableEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)
[**WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend) 
 [ **WdfRequestStopAcknowledge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)
[**WdfWorkItemEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)
 

 





