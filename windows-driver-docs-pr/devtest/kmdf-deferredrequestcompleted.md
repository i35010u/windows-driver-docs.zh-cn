---
title: DeferredRequestCompleted 规则（kmdf）
description: DeferredRequestCompleted 规则指定，如果向驱动程序的默认 i/o 队列提供的 i/o 请求未在回调函数中完成，但已延迟以便以后处理，则必须在延迟处理回调函数中完成该请求，除非将该请求转发和传递到框架，或除非调用 WdfRequestStopAcknowledge 方法。
ms.assetid: 14ed0dda-8acb-48fe-933f-e498c41f5403
ms.date: 05/21/2018
keywords:
- DeferredRequestCompleted 规则（kmdf）
topic_type:
- apiref
api_name:
- DeferredRequestCompleted
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f698bfcb3314a4ef6ab2eccbce5f1ca119935ce9
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918029"
---
# <a name="deferredrequestcompleted-rule-kmdf"></a>DeferredRequestCompleted 规则（kmdf）


**DeferredRequestCompleted**规则指定，如果向驱动程序的默认 i/o 队列提供的 i/o 请求未在回调函数中完成，但已延迟以便以后处理，则必须在延迟处理回调函数中完成该请求，除非将该请求转发和传递到框架，或除非调用[**WdfRequestStopAcknowledge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)方法。

**DeferredRequestCompleted**规则要求使用** \_ \_ sdv \_ save \_ 请求**和** \_ \_ sdv \_ 检索 \_ 请求**宏来识别延迟的请求。 有关如何使用这些宏的详细信息，请参阅对[ \_ \_ \_ \_ \_ \_ \_ \_ 延迟过程调用使用 sdv save request 和 sdv 检索请求](https://docs.microsoft.com/windows-hardware/drivers/devtest/using---sdv-save-request-and---sdv-retrieve-request-for-deferred-proce)。 前提条件规则**AliasWithinTimerDpc**检查是否存在这些宏。

在从 i/o 请求函数（在以下情况下除外）退出之前，必须先完成通过其中一个队列回调函数向驱动程序的默认队列提供的请求并将其完成：

-   已将 i/o 请求转发到 i/o 目标或其他队列

-   I/o 请求已传递到框架（通过调用[**WdfDeviceEnqueueRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)）

-   已调用**WdfRequestStopAcknowledge**方法

当驱动程序退出以下回调函数时，验证规则：

-   队列的**EvtIoStop**、 **EvtCleanupCallback**或**EvtDestroyCallback**

-   File 对象的**EvtCleanupCallback**或**EvtDestroyCallback**

-   **EvtFileClose**、 **EvtFileCleanup**、 **EvtDeviceSelfManagedIoSuspend**、 **EvtDeviceSelfManagedIoFlush**、 **EvtDeviceSelfManagedIoCleanup**、 **EvtDeviceShutdownNotification**、 **EvtDeviceSurpriseRemoval**、 **EvtCleanupCallback**或**EvtDestroyCallback**用于设备

-   **EvtDriverUnload**

I/o 请求表示形式的 i/o 队列回调函数包括**EvtIoDefault**、 **EvtIoRead**、 **EvtIoWrite**、 **EvtIoDeviceControl**和**EvtIoInternalDeviceControl**。

I/o 请求的延迟处理回调函数为**EvtTimerFunc**、 **EvtDpcFunc**、 **EvtInterruptDpc**、 **EvtInterruptEnable**、 **EvtInterruptDisable**和**EvtWorkItem**。

**DeferredRequestCompleted**规则使用对**WdfRequestMarkCancelable**、 **WdfDmaTransactionInitializeUsingRequest**、 **WdfDmaTransactionInitialize**或**WdfWorkItemEnqueue**方法的调用来指示正在延迟 i/o 请求。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>DeferredRequestCompleted</strong>规则。</p>
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

[**WdfDeviceEnqueueRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest) 
[**WdfDmaTransactionInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize) 
[**WdfDmaTransactionInitializeUsingRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingrequest) 
[**WdfIoTargetSendInternalIoctlOthersSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously) 
[**WdfIoTargetSendInternalIoctlSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously) 
[**WdfIoTargetSendIoctlSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously) 
[**WdfIoTargetSendReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously) 
[**WdfIoTargetSendWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously) 
[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 
[**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation) 
[**WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) 
[**WdfRequestForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue) 
[**WdfRequestMarkCancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable) 
[**WdfRequestMarkCancelableEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex) 
[**WdfRequestSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 
[**WdfRequestStopAcknowledge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge) 
[**WdfRequestUnmarkCancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable) 
[**WdfWorkItemEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)
 

 





