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
ms.openlocfilehash: 9e82f7bc398cca3626b207be36fd80b16866e7f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368657"
---
# <a name="requestcompleted-rule-kmdf"></a>RequestCompleted 规则 (kmdf)


[ **DeferredRequestCompleted** ](kmdf-deferredrequestcompleted.md)规则指定，对于非筛选器驱动程序提供给驱动程序的默认 I/O 队列的每个请求必须完成，除非请求延迟或转发，或如果[ **WdfRequestStopAcknowledge** ](https://msdn.microsoft.com/library/windows/hardware/ff550033)调用。

在退出之前从 I/O 请求回调函数，除在以下情况下，必须完成 I/O 请求提供给驱动程序的默认队列通过队列回调函数之一：

-   请求已延迟 (到 DPC 或工作项，例如)。 在这种情况下，可以使用[DeferredRequestCompleted](kmdf-deferredrequestcompleted.md)规则。

-   请求已转发到 I/O 目标或另一个队列

-   请求已传递到框架 (通过调用[ **WdfDeviceEnqueueRequest**](https://msdn.microsoft.com/library/windows/hardware/ff545945))

-   [**WdfRequestStopAcknowledge** ](https://msdn.microsoft.com/library/windows/hardware/ff550033)调用

从以下的回调函数的驱动程序退出时验证规则：

-   [*EvtIoStop*](https://msdn.microsoft.com/library/windows/hardware/ff541788)， [ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)或者[ *EvtDestroyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540841)队列

-   [*EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)或[ *EvtDestroyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540841)文件对象

-   [*EvtFileClose*](https://msdn.microsoft.com/library/windows/hardware/ff541702)， [ *EvtFileCleanup*](https://msdn.microsoft.com/library/windows/hardware/ff541700)， [ *EvtDeviceSelfManagedIoSuspend*](https://msdn.microsoft.com/library/windows/hardware/ff540907)， [ *EvtDeviceSelfManagedIoFlush*](https://msdn.microsoft.com/library/windows/hardware/ff540901)， [ *EvtDeviceSelfManagedIoCleanup*](https://msdn.microsoft.com/library/windows/hardware/ff540898)， [ *EvtDeviceShutdownNotification*](https://msdn.microsoft.com/library/windows/hardware/ff540911)， [ *EvtDeviceSurpriseRemoval*](https://msdn.microsoft.com/library/windows/hardware/ff540913)， [ *EvtCleanupCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540840)或[ *EvtDestroyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540841)设备

-   [*EvtDriverUnload*](https://msdn.microsoft.com/library/windows/hardware/ff541694)

请求演示文稿的 I/O 队列回调函数是[ *EvtIoDefault*](https://msdn.microsoft.com/library/windows/hardware/ff541757)， [ *EvtIoRead*](https://msdn.microsoft.com/library/windows/hardware/ff541776)， [ *EvtIoWrite*](https://msdn.microsoft.com/library/windows/hardware/ff541813)， [ *EvtIoDeviceControl*](https://msdn.microsoft.com/library/windows/hardware/ff541758)，并[ *EvtIoInternalDeviceControl*](https://msdn.microsoft.com/library/windows/hardware/ff541768)

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>RequestCompleted</strong>规则。</p>
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
[**WdfWorkItemEnqueue**](https://msdn.microsoft.com/library/windows/hardware/ff551203)
 

 





