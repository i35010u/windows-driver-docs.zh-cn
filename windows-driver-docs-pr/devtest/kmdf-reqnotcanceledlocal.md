---
title: ReqNotCanceledLocal 规则 (kmdf)
description: ReqNotCanceledLocal 规则指定，是否标记为可取消的请求已完成默认 I/O 队列回调函数中，WdfRequestUnmarkCancelable 方法必须调用完成前在 I/O 请求。
ms.assetid: 3cc3d517-6fb9-46b2-9d22-6bdbef442007
ms.date: 05/21/2018
keywords:
- ReqNotCanceledLocal 规则 (kmdf)
topic_type:
- apiref
api_name:
- ReqNotCanceledLocal
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c4c3a305e67c7b19f061feda6cd009c710ef4f37
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392916"
---
# <a name="reqnotcanceledlocal-rule-kmdf"></a>ReqNotCanceledLocal 规则 (kmdf)


**ReqNotCanceledLocal**规则指定，是否请求标记为可取消它完成在默认 I/O 队列回调函数中， [ **WdfRequestUnmarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)上的 I/O 请求完成之前，必须在调用方法。 必须完成的 I/O 请求，除非调用之前，会取消该请求**WdfRequestUnmarkCancelable**。

如果被标记为可通过取消请求[ **WdfRequestMarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)已完成 (通过调用[ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)，[ **WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)，或[ **WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost))， [ **WdfRequestUnmarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable) I/O 请求完成之前，必须在调用方法。 可以完成该请求，除非**WdfRequestUnmarkCancelable**方法将返回状态，它等于**状态\_已取消**。

请求的默认 I/O 队列回调函数是[ *EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)， [ *EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)， [ *EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)， [ *EvtIoDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)， [ *EvtIoInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control).

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>ReqNotCanceledLocal</strong>规则。</p>
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

[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)
[**WdfRequestCompleteWithInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation) 
 [ **WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)
[**WdfRequestMarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable) 
 [ **WdfRequestMarkCancelableEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)
[**WdfRequestUnmarkCancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)
 

 





