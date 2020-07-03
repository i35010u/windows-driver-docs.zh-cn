---
title: NoIoQueuePurgeSynchronously 规则（kmdf）
ms.assetid: 9255C644-1141-4D9A-8B84-BF98FB9E262A
ms.date: 05/21/2018
description: ''
keywords:
- NoIoQueuePurgeSynchronously 规则（kmdf）
topic_type:
- apiref
api_name:
- NoIoQueuePurgeSynchronously
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ab05178035f6302bce15c3b688ac94f6f04b9f10
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916289"
---
# <a name="noioqueuepurgesynchronously-rule-kmdf"></a>NoIoQueuePurgeSynchronously 规则（kmdf）


**NoIoQueuePurgeSynchronously**规则验证 WDF 驱动程序不会从以下 WdfIoQueuePurgeSynchronously 队列对象事件回调函数调用[**WdfIoQueueStopSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopsynchronously)、 [**WdfIoQueueDrainSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)、 [**WdfIoQueueStopAndPurgeSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously)或[**EvtIO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurgesynchronously)函数：

[*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default) 
[*EvtIoDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control) 
[*EvtIoInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control) 
[*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read) 
[*EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>NoIoQueuePurgeSynchronously</strong>规则。</p>
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

[**WdfRequestCancelSentRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest) 
[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 
[**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation) 
[**WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) 
[**WdfRequestMarkCancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable) 
[**WdfRequestMarkCancelableEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex) 
[**WdfRequestStopAcknowledge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge) 
[**WdfRequestUnmarkCancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)








