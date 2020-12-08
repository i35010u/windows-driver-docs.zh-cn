---
title: RequestProcessing 规则集 (KMDF)
description: 使用这些规则验证驱动程序是否正确完成或取消 (IRP) 的 i/o 请求包。
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1421603d56ec9f0b3d37e42a2310eeaae7eeecf2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836835"
---
# <a name="requestprocessing-rule-set-kmdf"></a>RequestProcessing 规则集 (KMDF)


使用这些规则验证驱动程序是否正确完成或取消 (IRP) 的 i/o 请求包。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="kmdf-changequeuestate.md" data-raw-source="[&lt;strong&gt;ChangeQueueState&lt;/strong&gt;](kmdf-changequeuestate.md)"><strong>ChangeQueueState</strong></a></p></td>
<td align="left"><p><a href="kmdf-changequeuestate.md" data-raw-source="[&lt;strong&gt;ChangeQueueState&lt;/strong&gt;](kmdf-changequeuestate.md)"><strong>ChangeQueueState</strong></a>规则指定 WDF 驱动程序不会尝试更改并发线程的队列状态，也不会从同一线程内的另一次调用状态更改 DDIs。 队列状态更改回调函数为 <a href="/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop" data-raw-source="[&lt;strong&gt;WdfIoQueueStop&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop)"><strong>WdfIoQueueStop</strong></a>、 <a href="/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopsynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueStopSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopsynchronously)"><strong>WdfIoQueueStopSynchronously</strong></a>、<a href="/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurge" data-raw-source="[&lt;strong&gt;WdfIoQueuePurge&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurge)"><strong>WdfIoQueuePurge</strong></a>、<a href="/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurgesynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueuePurgeSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurgesynchronously)"><strong>WdfIoQueuePurgeSynchronously</strong></a>、 <a href="/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrain" data-raw-source="[&lt;strong&gt;WdfIoQueueDrain&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrain)"><strong>WdfIoQueueDrain</strong></a>、 <a href="/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrainsynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueDrainSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)"><strong>WdfIoQueueDrainSynchronously</strong></a>、 <a href="/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurge" data-raw-source="[&lt;strong&gt;WdfIoQueueStopAndPurge&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurge)"><strong>WdfIoQueueStopAndPurge</strong></a> 和 <a href="/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueStopAndPurgeSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously)"><strong>WdfIoQueueStopAndPurgeSynchronously</strong></a>。 如果在队列状态更改已经正在进行时调用这些 DDIs，将导致计算机崩溃或停止响应。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-completecanceledreq.md" data-raw-source="[&lt;strong&gt;CompleteCanceledReq&lt;/strong&gt;](kmdf-completecanceledreq.md)"><strong>CompleteCanceledReq</strong></a></p></td>
<td align="left"><p><a href="kmdf-completecanceledreq.md" data-raw-source="[&lt;strong&gt;CompleteCanceledReq&lt;/strong&gt;](kmdf-completecanceledreq.md)"><strong>CompleteCanceledReq</strong></a>规则指定如果请求已取消，请求将不再有效，驱动程序不应完成该请求。 尽管驱动程序取消了之前标记为可取消的请求，但它必须检查请求是否已取消。 如果驱动程序没有进行此检查，驱动程序可能会完成已释放的请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-doublecompletion.md" data-raw-source="[&lt;strong&gt;DoubleCompletion&lt;/strong&gt;](kmdf-doublecompletion.md)"><strong>DoubleCompletion</strong></a></p></td>
<td align="left"><p><a href="kmdf-doublecompletion.md" data-raw-source="[&lt;strong&gt;DoubleCompletion&lt;/strong&gt;](kmdf-doublecompletion.md)"><strong>DoubleCompletion</strong></a>规则指定驱动程序不得完成 i/o 请求两次。 对于同一请求，不应在一行中调用以下方法两次： <a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete" data-raw-source="[&lt;strong&gt;WdfRequestComplete&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)"><strong>WdfRequestComplete</strong></a>、 <a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation" data-raw-source="[&lt;strong&gt;WdfRequestCompleteWithInformation&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)"><strong>WdfRequestCompleteWithInformation</strong></a>、 <a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost" data-raw-source="[&lt;strong&gt;WdfRequestCompleteWithPriorityBoost&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)"><strong>WdfRequestCompleteWithPriorityBoost</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-doublecompletionlocal.md" data-raw-source="[&lt;strong&gt;DoubleCompletionLocal&lt;/strong&gt;](kmdf-doublecompletionlocal.md)"><strong>DoubleCompletionLocal</strong></a></p></td>
<td align="left"><p><a href="kmdf-doublecompletionlocal.md" data-raw-source="[DoubleCompletionLocal](kmdf-doublecompletionlocal.md)">DoubleCompletionLocal</a>规则指定驱动程序不得完成 i/o 请求两次。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-evtiostopcancel.md" data-raw-source="[&lt;strong&gt;EvtIoStopCancel&lt;/strong&gt;](kmdf-evtiostopcancel.md)"><strong>EvtIoStopCancel</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtiostopcancel.md" data-raw-source="[&lt;strong&gt;EvtIoStopCancel&lt;/strong&gt;](kmdf-evtiostopcancel.md)"><strong>EvtIoStopCancel</strong></a>规则指定在<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a>回调函数中，驱动程序为不可取消的 i/o 请求调用以下方法之一。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-evtiostopcompleteorstopack.md" data-raw-source="[&lt;strong&gt;EvtIoStopCompleteOrStopAck&lt;/strong&gt;](kmdf-evtiostopcompleteorstopack.md)"><strong>EvtIoStopCompleteOrStopAck</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtiostopcompleteorstopack.md" data-raw-source="[&lt;strong&gt;EvtIoStopCompleteOrStopAck&lt;/strong&gt;](kmdf-evtiostopcompleteorstopack.md)"><strong>EvtIoStopCompleteOrStopAck</strong></a>规则指定在<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a>回调函数中，驱动程序为框架提供的每个 i/o 请求调用以下方法之一。 如果未执行此操作，驱动程序可能会阻止系统进入另一个低功率状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-evtsurpriseremovenosuspendqueue.md" data-raw-source="[&lt;strong&gt;EvtSurpriseRemoveNoSuspendQueue&lt;/strong&gt;](kmdf-evtsurpriseremovenosuspendqueue.md)"><strong>EvtSurpriseRemoveNoSuspendQueue</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtsurpriseremovenosuspendqueue.md" data-raw-source="[&lt;strong&gt;EvtSurpriseRemoveNoSuspendQueue&lt;/strong&gt;](kmdf-evtsurpriseremovenosuspendqueue.md)"><strong>EvtSurpriseRemoveNoSuspendQueue</strong></a>规则指定 WDF 驱动程序不应使用<a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)"><em>EvtDeviceSurpriseRemoval</em></a>回调函数排出、停止或清除队列，而应使用自托管 i/o 回调函数。 <em>EvtDeviceSurpriseRemoval</em>回调函数未与电源线路径同步。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-fileobjectconfigured.md" data-raw-source="[&lt;strong&gt;FileObjectConfigured&lt;/strong&gt;](kmdf-fileobjectconfigured.md)"><strong>FileObjectConfigured</strong></a></p></td>
<td align="left"><p><a href="kmdf-fileobjectconfigured.md" data-raw-source="[&lt;strong&gt;FileObjectConfigured&lt;/strong&gt;](kmdf-fileobjectconfigured.md)"><strong>FileObjectConfigured</strong></a>规则指定对<a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetfileobject" data-raw-source="[&lt;strong&gt;WdfRequestGetFileObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetfileobject)"><strong>WdfRequestGetFileObject</strong></a>方法的调用，前面是对<a href="/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig" data-raw-source="[&lt;strong&gt;WdfDeviceInitSetFileObjectConfig&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)"><strong>WdfDeviceInitSetFileObjectConfig</strong></a>的调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-internalioctlreqs.md" data-raw-source="[&lt;strong&gt;InternalIoctlReqs&lt;/strong&gt;](kmdf-internalioctlreqs.md)"><strong>InternalIoctlReqs</strong></a></p></td>
<td align="left"><p><a href="kmdf-internalioctlreqs.md" data-raw-source="[&lt;strong&gt;InternalIoctlReqs&lt;/strong&gt;](kmdf-internalioctlreqs.md)"><strong>InternalIoctlReqs</strong></a>规则指定内部 IOCTL 请求不会传递到不适当的 KMDF 请求-发送设备驱动程序接口 (DDIs) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-invalidreqaccess.md" data-raw-source="[&lt;strong&gt;InvalidReqAccess&lt;/strong&gt;](kmdf-invalidreqaccess.md)"><strong>InvalidReqAccess</strong></a></p></td>
<td align="left"><p><a href="kmdf-invalidreqaccess.md" data-raw-source="[&lt;strong&gt;InvalidReqAccess&lt;/strong&gt;](kmdf-invalidreqaccess.md)"><strong>InvalidReqAccess</strong></a>规则指定在完成或取消请求后，不会对其进行访问。 此规则可能与其他规则重叠，如检查双重完成的规则或检查请求的规则是否已标记为可取消两次。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-invalidreqaccesslocal.md" data-raw-source="[&lt;strong&gt;InvalidReqAccessLocal&lt;/strong&gt;](kmdf-invalidreqaccesslocal.md)"><strong>InvalidReqAccessLocal</strong></a></p></td>
<td align="left"><p><a href="kmdf-invalidreqaccesslocal.md" data-raw-source="[&lt;strong&gt;InvalidReqAccessLocal&lt;/strong&gt;](kmdf-invalidreqaccesslocal.md)"><strong>InvalidReqAccessLocal</strong></a>规则指定在完成或取消本地创建的请求后，不会对其进行访问。 此规则可能与其他规则重叠，如检查双重完成的规则或检查请求的规则是否已标记为可取消两次。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-ioctlreqs.md" data-raw-source="[&lt;strong&gt;IoctlReqs&lt;/strong&gt;](kmdf-ioctlreqs.md)"><strong>IoctlReqs</strong></a></p></td>
<td align="left"><p><a href="kmdf-ioctlreqs.md" data-raw-source="[&lt;strong&gt;IoctlReqs&lt;/strong&gt;](kmdf-ioctlreqs.md)"><strong>IoctlReqs</strong></a>规则指定不能将 IOCTL 请求传递到不适当的 KMDF 请求或 (DDIs) 发送设备驱动程序接口。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-markcanconcancreqlocal.md" data-raw-source="[&lt;strong&gt;MarkCancOnCancReqLocal&lt;/strong&gt;](kmdf-markcanconcancreqlocal.md)"><strong>MarkCancOnCancReqLocal</strong></a></p></td>
<td align="left"><p><a href="kmdf-markcanconcancreqlocal.md" data-raw-source="[&lt;strong&gt;MarkCancOnCancReqLocal&lt;/strong&gt;](kmdf-markcanconcancreqlocal.md)"><strong>MarkCancOnCancReqLocal</strong></a>规则指定在同一 i/o 请求上不能连续调用<a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable" data-raw-source="[&lt;strong&gt;WdfRequestMarkCancelable&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)"><strong>WdfRequestMarkCancelable</strong></a>方法两次。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="noioqueuepurgesynchronously.md" data-raw-source="[&lt;strong&gt;NoIoQueuePurgeSynchronously&lt;/strong&gt;](noioqueuepurgesynchronously.md)"><strong>NoIoQueuePurgeSynchronously</strong></a></p></td>
<td align="left"><p><a href="noioqueuepurgesynchronously.md" data-raw-source="[&lt;strong&gt;NoIoQueuePurgeSynchronously&lt;/strong&gt;](noioqueuepurgesynchronously.md)"><strong>NoIoQueuePurgeSynchronously</strong></a>规则验证 WDF 驱动程序不会从以下 WdfIoQueuePurgeSynchronously 队列对象事件回调函数调用<a href="/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopsynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueStopSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopsynchronously)"><strong>WdfIoQueueStopSynchronously</strong></a>、 <a href="/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrainsynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueDrainSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)"><strong>WdfIoQueueDrainSynchronously</strong></a>、 <a href="/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueStopAndPurgeSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously)"><strong>WdfIoQueueStopAndPurgeSynchronously</strong></a>或<a href="/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurgesynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueuePurgeSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuepurgesynchronously)"><strong>EvtIO</strong></a>函数：</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-outputbufferapi.md" data-raw-source="[&lt;strong&gt;OutputBufferAPI&lt;/strong&gt;](kmdf-outputbufferapi.md)"><strong>OutputBufferAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-outputbufferapi.md" data-raw-source="[&lt;strong&gt;OutputBufferAPI&lt;/strong&gt;](kmdf-outputbufferapi.md)"><strong>OutputBufferAPI</strong></a>规则指定在<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"><em>EvtIoWrite</em></a>回调函数中使用正确的缓冲区检索 DDIs。 在 <em>EvtIoWrite</em> 回调函数中，不能调用以下 DDIs 进行缓冲区检索：</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-readreqs.md" data-raw-source="[&lt;strong&gt;ReadReqs&lt;/strong&gt;](kmdf-readreqs.md)"><strong>ReadReqs</strong></a></p></td>
<td align="left"><p><a href="kmdf-readreqs.md" data-raw-source="[&lt;strong&gt;ReadReqs&lt;/strong&gt;](kmdf-readreqs.md)"><strong>ReadReqs</strong></a>规则指定读取请求不会传递到不适当的 KMDF 方法。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-reqcompletionroutine.md" data-raw-source="[&lt;strong&gt;ReqCompletionRoutine&lt;/strong&gt;](kmdf-reqcompletionroutine.md)"><strong>ReqCompletionRoutine</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqcompletionroutine.md" data-raw-source="[&lt;strong&gt;ReqCompletionRoutine&lt;/strong&gt;](kmdf-reqcompletionroutine.md)"><strong>ReqCompletionRoutine</strong></a>规则指定在向 i/o 目标发送请求之前必须设置完成例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-reqdelete.md" data-raw-source="[&lt;strong&gt;ReqDelete&lt;/strong&gt;](kmdf-reqdelete.md)"><strong>ReqDelete</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqdelete.md" data-raw-source="[&lt;strong&gt;ReqDelete&lt;/strong&gt;](kmdf-reqdelete.md)"><strong>ReqDelete</strong></a>规则指定不向<em>WdfRequestCompleteXxx</em>函数传递驱动程序创建的请求。 相反，请求应在完成时删除。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-reqiscanconcancreq.md" data-raw-source="[&lt;strong&gt;ReqIsCancOnCancReq&lt;/strong&gt;](kmdf-reqiscanconcancreq.md)"><strong>ReqIsCancOnCancReq</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqiscanconcancreq.md" data-raw-source="[&lt;strong&gt;ReqIsCancOnCancReq&lt;/strong&gt;](kmdf-reqiscanconcancreq.md)"><strong>ReqIsCancOnCancReq</strong></a>规则指定只能对未标记为可取消的请求调用<a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestiscanceled" data-raw-source="[&lt;strong&gt;WdfRequestIsCanceled&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestiscanceled)"><strong>WdfRequestIsCanceled</strong></a>方法。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-reqmarkcancelablesend.md" data-raw-source="[&lt;strong&gt;ReqMarkCancelableSend&lt;/strong&gt;](kmdf-reqmarkcancelablesend.md)"><strong>ReqMarkCancelableSend</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqmarkcancelablesend.md" data-raw-source="[&lt;strong&gt;ReqMarkCancelableSend&lt;/strong&gt;](kmdf-reqmarkcancelablesend.md)"><strong>ReqMarkCancelableSend</strong></a>规则指定通过调用<a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable" data-raw-source="[&lt;strong&gt;WdfRequestMarkCancelable&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)"><strong>WdfRequestMarkCancelable</strong></a>，驱动程序转发的请求未标记为可取消。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-requestcompleted.md" data-raw-source="[&lt;strong&gt;RequestCompleted&lt;/strong&gt;](kmdf-requestcompleted.md)"><strong>RequestCompleted</strong></a></p></td>
<td align="left"><p><a href="kmdf-deferredrequestcompleted.md" data-raw-source="[&lt;strong&gt;DeferredRequestCompleted&lt;/strong&gt;](kmdf-deferredrequestcompleted.md)"><strong>DeferredRequestCompleted</strong></a>规则指定对于非筛选器驱动程序，必须完成提供给该驱动程序的默认 i/o 队列的每个请求，除非该请求被延迟或转发，或者调用<a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge" data-raw-source="[&lt;strong&gt;WdfRequestStopAcknowledge&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)"><strong>WdfRequestStopAcknowledge</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-requestformattedvalid.md" data-raw-source="[&lt;strong&gt;RequestFormattedValid&lt;/strong&gt;](kmdf-requestformattedvalid.md)"><strong>RequestFormattedValid</strong></a></p></td>
<td align="left"><p><a href="kmdf-requestformattedvalid.md" data-raw-source="[&lt;strong&gt;RequestFormattedValid&lt;/strong&gt;](kmdf-requestformattedvalid.md)"><strong>RequestFormattedValid</strong></a>规则指定在将请求发送到 i/o 目标之前，驱动程序将设置所有请求的格式，但 WDF_REQUEST_SEND_OPTION_SEND_AND_FORGET 请求除外。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-requestgetstatusvalid.md" data-raw-source="[&lt;strong&gt;RequestGetStatusValid&lt;/strong&gt;](kmdf-requestgetstatusvalid.md)"><strong>RequestGetStatusValid</strong></a></p></td>
<td align="left"><p><a href="kmdf-requestgetstatusvalid.md" data-raw-source="[&lt;strong&gt;RequestGetStatusValid&lt;/strong&gt;](kmdf-requestgetstatusvalid.md)"><strong>RequestGetStatusValid</strong></a>规则，该规则指定应在下列情况之一为请求调用<a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetstatus" data-raw-source="[&lt;strong&gt;WdfRequestGetStatus&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetstatus)"><strong>WdfRequestGetStatus</strong></a> ：</p>
<ul>
<li>当 <a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)"><strong>WdfRequestSend</strong></a> 返回失败时。</li>
<li>请求发送 WDF_REQUEST_SEND_OPTION_SYNCHRONOUS。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-requestsendandforgetnoformatting.md" data-raw-source="[&lt;strong&gt;RequestSendAndForgetNoFormatting&lt;/strong&gt;](kmdf-requestsendandforgetnoformatting.md)"><strong>RequestSendAndForgetNoFormatting</strong></a></p></td>
<td align="left"><p><a href="kmdf-requestsendandforgetnoformatting.md" data-raw-source="[&lt;strong&gt;RequestSendAndForgetNoFormatting&lt;/strong&gt;](kmdf-requestsendandforgetnoformatting.md)"><strong>RequestSendAndForgetNoFormatting</strong></a>规则验证驱动程序在将请求发送到具有 send 选项 WDF_REQUEST_SEND_OPTION_SEND_AND_FORGET 的 i/o 目标之前，不会使用 i/o 目标格式设置函数对请求进行格式设置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-requestsendandforgetnoformatting2.md" data-raw-source="[&lt;strong&gt;RequestSendAndForgetNoFormatting2&lt;/strong&gt;](kmdf-requestsendandforgetnoformatting2.md)"><strong>RequestSendAndForgetNoFormatting2</strong></a></p></td>
<td align="left"><p><a href="kmdf-requestsendandforgetnoformatting2.md" data-raw-source="[&lt;strong&gt;RequestSendAndForgetNoFormatting2&lt;/strong&gt;](kmdf-requestsendandforgetnoformatting2.md)"><strong>RequestSendAndForgetNoFormatting2</strong></a>规则验证驱动程序在将请求发送到具有 send 选项 WDF_REQUEST_SEND_OPTION_SEND_AND_FORGET 的 i/o 目标之前，不会使用 i/o 目标格式设置函数对请求进行格式设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-stopackwithinevtiostop.md" data-raw-source="[&lt;strong&gt;StopAckWithinEvtIoStop&lt;/strong&gt;](kmdf-stopackwithinevtiostop.md)"><strong>StopAckWithinEvtIoStop</strong></a></p></td>
<td align="left"><p><a href="kmdf-stopackwithinevtiostop.md" data-raw-source="[&lt;strong&gt;StopAckWithinEvtIoStop&lt;/strong&gt;](kmdf-stopackwithinevtiostop.md)"><strong>StopAckWithinEvtIoStop</strong></a>规则指定仅从<a href="/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>EvtIoStop</em></a>回调函数内调用<a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge" data-raw-source="[&lt;strong&gt;WdfRequestStopAcknowledge&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)"><strong>WdfRequestStopAcknowledge</strong></a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfioqueuefindrequestfailed.md" data-raw-source="[&lt;strong&gt;WdfIoQueueFindRequestFailed&lt;/strong&gt;](kmdf-wdfioqueuefindrequestfailed.md)"><strong>WdfIoQueueFindRequestFailed</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfioqueuefindrequestfailed.md" data-raw-source="[&lt;strong&gt;WdfIoQueueFindRequestFailed&lt;/strong&gt;](kmdf-wdfioqueuefindrequestfailed.md)"><strong>WdfIoQueueFindRequestFailed</strong></a>规则指定仅应在<strong>WdfIoQueueFindRequestFailed</strong>返回 STATUS_SUCCESS 之后调用<a href="kmdf-wdfioqueueretrievefoundrequest.md" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveFoundRequest&lt;/strong&gt;](kmdf-wdfioqueueretrievefoundrequest.md)"><strong>WdfIoQueueRetrieveFoundRequest</strong></a>或<a href="/windows-hardware/drivers/wdf/wdfobjectdereference" data-raw-source="[&lt;strong&gt;WdfObjectDereference&lt;/strong&gt;](../wdf/wdfobjectdereference.md)"><strong>WdfObjectDereference</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-wdfioqueueretrievefoundrequest.md" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveFoundRequest&lt;/strong&gt;](kmdf-wdfioqueueretrievefoundrequest.md)"><strong>WdfIoQueueRetrieveFoundRequest</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfioqueueretrievefoundrequest.md" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveFoundRequest&lt;/strong&gt;](kmdf-wdfioqueueretrievefoundrequest.md)"><strong>WdfIoQueueRetrieveFoundRequest</strong></a>规则指定仅在调用<a href="/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuefindrequest" data-raw-source="[&lt;strong&gt;WdfIoQueueFindRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuefindrequest)"><strong>WdfIoQueueFindRequest</strong></a>并 STATUS_SUCCESS，并在同一请求上调用 WdfIoQueueRetrieveFoundRequest<a href="/windows-hardware/drivers/wdf/wdfobjectdereference" data-raw-source="[&lt;strong&gt;WdfObjectDereference&lt;/strong&gt;](../wdf/wdfobjectdereference.md)"><strong>方法时调用</strong></a> <a href="/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveFoundRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest)"><strong>WdfIoQueueRetrieveFoundRequest</strong></a>方法。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfioqueueretrievenextrequest.md" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveNextRequest&lt;/strong&gt;](kmdf-wdfioqueueretrievenextrequest.md)"><strong>WdfIoQueueRetrieveNextRequest</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfioqueueretrievenextrequest.md" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveNextRequest&lt;/strong&gt;](kmdf-wdfioqueueretrievenextrequest.md)"><strong>WdfIoQueueRetrieveNextRequest</strong></a>规则指定在调用<a href="/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuefindrequest" data-raw-source="[&lt;strong&gt;WdfIoQueueFindRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuefindrequest)"><strong>WdfIoQueueFindRequest</strong></a>后不调用<a href="/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievenextrequest" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveNextRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievenextrequest)"><strong>WdfIoQueueRetrieveNextRequest</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-writereqs.md" data-raw-source="[&lt;strong&gt;WriteReqs&lt;/strong&gt;](kmdf-writereqs.md)"><strong>WriteReqs</strong></a></p></td>
<td align="left"><p><a href="kmdf-writereqs.md" data-raw-source="[&lt;strong&gt;WriteReqs&lt;/strong&gt;](kmdf-writereqs.md)"><strong>WriteReqs</strong></a>规则指定不将写入请求传递到不适当的 KMDF 方法。</p></td>
</tr>
</tbody>
</table>

 

**选择 RequestProcessing 规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 **RequestProcessing**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check** 选项指定 **RequestProcessing。 sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:RequestProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

