---
title: DeferredRequestCompleted 规则 (kmdf)
description: DeferredRequestCompleted 规则指定，是否提供给驱动程序的默认 I/O 队列的 I/O 请求未完成回调函数中，但以供将来处理延迟，请求必须完成中的延迟的处理回调函数，除非请求将转发并传递到框架，或者调用 WdfRequestStopAcknowledge 方法。
ms.assetid: 14ed0dda-8acb-48fe-933f-e498c41f5403
ms.date: 05/21/2018
keywords:
- DeferredRequestCompleted 规则 (kmdf)
topic_type:
- apiref
api_name:
- DeferredRequestCompleted
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 96a4a462b858be1d066a6a8e587eaa4b2007d26a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340357"
---
# <a name="deferredrequestcompleted-rule-kmdf"></a>DeferredRequestCompleted 规则 (kmdf)


**DeferredRequestCompleted**规则指定是否驱动程序的默认 I/O 队列向显示的 I/O 请求未完成回调函数中，但以供将来处理延迟，必须完成该请求以延迟处理回调函数，除非请求将转发并传递到框架，或者[ **WdfRequestStopAcknowledge** ](https://msdn.microsoft.com/library/windows/hardware/ff550033)调用方法。

**DeferredRequestCompleted**规则需要识别使用延迟的请求 **\_ \_sdv\_保存\_请求**和 **\_ \_sdv\_检索\_请求**宏。 有关如何使用这些宏的信息，请参阅[Using \_ \_sdv\_保存\_请求并\_ \_sdv\_检索\_为请求延迟过程调用](https://msdn.microsoft.com/library/windows/hardware/ff556071)。 不满足前提条件规则**AliasWithinTimerDpc**检查是否存在这些宏。

在退出之前从 I/O 请求回调函数，除在以下情况下，必须完成的请求提供给通过队列回调函数之一的驱动程序的默认队列和延迟:

-   I/O 请求已转发到 I/O 目标或另一个队列

-   I/O 请求已传递到框架 (通过调用[ **WdfDeviceEnqueueRequest**](https://msdn.microsoft.com/library/windows/hardware/ff545945))

-   **WdfRequestStopAcknowledge**调用方法

从以下的回调函数的驱动程序退出时验证规则：

-   **EvtIoStop**， **EvtCleanupCallback**或**EvtDestroyCallback**队列

-   **EvtCleanupCallback**或**EvtDestroyCallback**文件对象

-   **EvtFileClose**， **EvtFileCleanup**， **EvtDeviceSelfManagedIoSuspend**， **EvtDeviceSelfManagedIoFlush**， **EvtDeviceSelfManagedIoCleanup**， **EvtDeviceShutdownNotification**， **EvtDeviceSurpriseRemoval**， **EvtCleanupCallback**或**EvtDestroyCallback**设备

-   **EvtDriverUnload**

对 i/o 的 I/O 队列回调函数请求是演示文稿**EvtIoDefault**， **EvtIoRead**， **EvtIoWrite**， **EvtIoDeviceControl**，并**EvtIoInternalDeviceControl**。

I/O 请求的延迟的处理回调函数是**EvtTimerFunc**， **EvtDpcFunc**， **EvtInterruptDpc**， **EvtInterruptEnable**， **EvtInterruptDisable**，和**EvtWorkItem**。

**DeferredRequestCompleted**规则使用调用**WdfRequestMarkCancelable**， **WdfDmaTransactionInitializeUsingRequest**， **WdfDmaTransactionInitialize**，或**WdfWorkItemEnqueue**方法，以指示 I/O 请求被延迟。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>DeferredRequestCompleted</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**WdfDeviceEnqueueRequest**](https://msdn.microsoft.com/library/windows/hardware/ff545945)
[**WdfDmaTransactionInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff547099) 
 [ **WdfDmaTransactionInitializeUsingRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547107)
[**WdfIoTargetSendInternalIoctlOthersSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548651) 
[ **WdfIoTargetSendInternalIoctlSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548656)
[**WdfIoTargetSendIoctlSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548660) 
 [ **WdfIoTargetSendReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548669)
[**WdfIoTargetSendWriteSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548672) 
 [ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948) 
 [ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) 
 [ **WdfRequestForwardToIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549958)
[**WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983) 
 [ **WdfRequestMarkCancelableEx**](https://msdn.microsoft.com/library/windows/hardware/ff549984)
[**WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027) 
 [ **WdfRequestStopAcknowledge**](https://msdn.microsoft.com/library/windows/hardware/ff550033)
[**WdfRequestUnmarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff550035)
 [ **WdfWorkItemEnqueue**](https://msdn.microsoft.com/library/windows/hardware/ff551203)
 

 





