---
title: RequestProcessing 规则集 (KMDF)
description: 使用这些规则来验证您的驱动程序正确完成或取消 I/O 请求数据包 (IRP)。
ms.assetid: 25162982-6A98-4018-82B3-8DD3E0A0A002
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1827342eaa276ae52419335ebe124161e5821bc9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353875"
---
# <a name="requestprocessing-rule-set-kmdf"></a>RequestProcessing 规则集 (KMDF)


使用这些规则来验证您的驱动程序正确完成或取消 I/O 请求数据包 (IRP)。

## <a name="in-this-section"></a>本节内容


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
<td align="left"><p><a href="kmdf-changequeuestate.md" data-raw-source="[&lt;strong&gt;ChangeQueueState&lt;/strong&gt;](kmdf-changequeuestate.md)"> <strong>ChangeQueueState</strong> </a>规则指定 WDF 驱动程序不会尝试从并发线程更改队列的状态或不会调用 DDIs 一个接一个从更改中相同的状态线程。 队列的状态不断变化的回调函数非常<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestop" data-raw-source="[&lt;strong&gt;WdfIoQueueStop&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestop)"> <strong>WdfIoQueueStop</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopsynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueStopSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopsynchronously)"> <strong>WdfIoQueueStopSynchronously</strong></a>，<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurge" data-raw-source="[&lt;strong&gt;WdfIoQueuePurge&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurge)"> <strong>WdfIoQueuePurge</strong></a>，<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurgesynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueuePurgeSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurgesynchronously)"><strong>WdfIoQueuePurgeSynchronously</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrain" data-raw-source="[&lt;strong&gt;WdfIoQueueDrain&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrain)"> <strong>WdfIoQueueDrain</strong> </a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrainsynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueDrainSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)"> <strong>WdfIoQueueDrainSynchronously</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopandpurge" data-raw-source="[&lt;strong&gt;WdfIoQueueStopAndPurge&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopandpurge)"> <strong>WdfIoQueueStopAndPurge</strong> </a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueStopAndPurgeSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously)"> <strong>WdfIoQueueStopAndPurgeSynchronously</strong></a>。 如果正在处理队列状态更改时调用这些 DDIs 它将导致计算机崩溃或停止响应。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-completecanceledreq.md" data-raw-source="[&lt;strong&gt;CompleteCanceledReq&lt;/strong&gt;](kmdf-completecanceledreq.md)"><strong>CompleteCanceledReq</strong></a></p></td>
<td align="left"><p><a href="kmdf-completecanceledreq.md" data-raw-source="[&lt;strong&gt;CompleteCanceledReq&lt;/strong&gt;](kmdf-completecanceledreq.md)"> <strong>CompleteCanceledReq</strong> </a>规则指定如果已取消请求，请求将不再有效，并且该驱动程序不应完成它。 在驱动程序会取消以前标记可取消的请求的标记，它必须检查，请求不已取消生成。 如果该驱动程序不会进行此检查，驱动程序可能完成的请求已释放。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-doublecompletion.md" data-raw-source="[&lt;strong&gt;DoubleCompletion&lt;/strong&gt;](kmdf-doublecompletion.md)"><strong>DoubleCompletion</strong></a></p></td>
<td align="left"><p><a href="kmdf-doublecompletion.md" data-raw-source="[&lt;strong&gt;DoubleCompletion&lt;/strong&gt;](kmdf-doublecompletion.md)"> <strong>DoubleCompletion</strong> </a>规则指定，驱动程序必须完成的 I/O 请求两次。 不应在同一请求的行中两次调用以下方法：<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete" data-raw-source="[&lt;strong&gt;WdfRequestComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)"><strong>WdfRequestComplete</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation" data-raw-source="[&lt;strong&gt;WdfRequestCompleteWithInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)"> <strong>WdfRequestCompleteWithInformation</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost" data-raw-source="[&lt;strong&gt;WdfRequestCompleteWithPriorityBoost&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)"> <strong>WdfRequestCompleteWithPriorityBoost</strong></a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-doublecompletionlocal.md" data-raw-source="[&lt;strong&gt;DoubleCompletionLocal&lt;/strong&gt;](kmdf-doublecompletionlocal.md)"><strong>DoubleCompletionLocal</strong></a></p></td>
<td align="left"><p><a href="kmdf-doublecompletionlocal.md" data-raw-source="[DoubleCompletionLocal](kmdf-doublecompletionlocal.md)">DoubleCompletionLocal</a>规则指定，驱动程序必须完成的 I/O 请求两次。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-evtiostopcancel.md" data-raw-source="[&lt;strong&gt;EvtIoStopCancel&lt;/strong&gt;](kmdf-evtiostopcancel.md)"><strong>EvtIoStopCancel</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtiostopcancel.md" data-raw-source="[&lt;strong&gt;EvtIoStopCancel&lt;/strong&gt;](kmdf-evtiostopcancel.md)"> <strong>EvtIoStopCancel</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"> <em>EvtIoStop</em> </a>回调函数，该驱动程序调用以下项之一是不可取消的 I/O 请求的方法。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-evtiostopcompleteorstopack.md" data-raw-source="[&lt;strong&gt;EvtIoStopCompleteOrStopAck&lt;/strong&gt;](kmdf-evtiostopcompleteorstopack.md)"><strong>EvtIoStopCompleteOrStopAck</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtiostopcompleteorstopack.md" data-raw-source="[&lt;strong&gt;EvtIoStopCompleteOrStopAck&lt;/strong&gt;](kmdf-evtiostopcompleteorstopack.md)"> <strong>EvtIoStopCompleteOrStopAck</strong> </a>规则指定，在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"> <em>EvtIoStop</em> </a>驱动程序的回调函数调用之一由框架显示每个 I/O 请求的以下方法。 如果不执行此操作，该驱动程序可能会阻止系统进入其他节能状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-evtsurpriseremovenosuspendqueue.md" data-raw-source="[&lt;strong&gt;EvtSurpriseRemoveNoSuspendQueue&lt;/strong&gt;](kmdf-evtsurpriseremovenosuspendqueue.md)"><strong>EvtSurpriseRemoveNoSuspendQueue</strong></a></p></td>
<td align="left"><p><a href="kmdf-evtsurpriseremovenosuspendqueue.md" data-raw-source="[&lt;strong&gt;EvtSurpriseRemoveNoSuspendQueue&lt;/strong&gt;](kmdf-evtsurpriseremovenosuspendqueue.md)"> <strong>EvtSurpriseRemoveNoSuspendQueue</strong> </a>规则指定 WDF 驱动程序不应清空、 停止或清除从队列<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal" data-raw-source="[&lt;em&gt;EvtDeviceSurpriseRemoval&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)"> <em>EvtDeviceSurpriseRemoval</em></a>回调函数，而是自托管 I/O 回调函数应使用。 <em>EvtDeviceSurpriseRemoval</em>回调函数不会同步与电源关闭路径。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-fileobjectconfigured.md" data-raw-source="[&lt;strong&gt;FileObjectConfigured&lt;/strong&gt;](kmdf-fileobjectconfigured.md)"><strong>FileObjectConfigured</strong></a></p></td>
<td align="left"><p><a href="kmdf-fileobjectconfigured.md" data-raw-source="[&lt;strong&gt;FileObjectConfigured&lt;/strong&gt;](kmdf-fileobjectconfigured.md)"> <strong>FileObjectConfigured</strong> </a>规则指定调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetfileobject" data-raw-source="[&lt;strong&gt;WdfRequestGetFileObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetfileobject)"> <strong>WdfRequestGetFileObject</strong> </a>方法前面通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig" data-raw-source="[&lt;strong&gt;WdfDeviceInitSetFileObjectConfig&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)"><strong>WdfDeviceInitSetFileObjectConfig</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-internalioctlreqs.md" data-raw-source="[&lt;strong&gt;InternalIoctlReqs&lt;/strong&gt;](kmdf-internalioctlreqs.md)"><strong>InternalIoctlReqs</strong></a></p></td>
<td align="left"><p><a href="kmdf-internalioctlreqs.md" data-raw-source="[&lt;strong&gt;InternalIoctlReqs&lt;/strong&gt;](kmdf-internalioctlreqs.md)"> <strong>InternalIoctlReqs</strong> </a>规则指定内部 IOCTL 请求不会传递到不适合 KMDF 发送的请求的设备驱动程序接口 (DDIs)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-invalidreqaccess.md" data-raw-source="[&lt;strong&gt;InvalidReqAccess&lt;/strong&gt;](kmdf-invalidreqaccess.md)"><strong>InvalidReqAccess</strong></a></p></td>
<td align="left"><p><a href="kmdf-invalidreqaccess.md" data-raw-source="[&lt;strong&gt;InvalidReqAccess&lt;/strong&gt;](kmdf-invalidreqaccess.md)"> <strong>InvalidReqAccess</strong> </a>规则指定后完成或取消不访问请求。 此规则与其他规则，例如，检查 double 完成状态的规则可能会重叠或检查请求的规则已标记为可取消两次。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-invalidreqaccesslocal.md" data-raw-source="[&lt;strong&gt;InvalidReqAccessLocal&lt;/strong&gt;](kmdf-invalidreqaccesslocal.md)"><strong>InvalidReqAccessLocal</strong></a></p></td>
<td align="left"><p><a href="kmdf-invalidreqaccesslocal.md" data-raw-source="[&lt;strong&gt;InvalidReqAccessLocal&lt;/strong&gt;](kmdf-invalidreqaccesslocal.md)"> <strong>InvalidReqAccessLocal</strong> </a>规则指定后完成或取消不访问本地创建的请求。 此规则与其他规则，例如，检查 double 完成状态的规则可能会重叠或检查请求的规则已标记为可取消两次。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-ioctlreqs.md" data-raw-source="[&lt;strong&gt;IoctlReqs&lt;/strong&gt;](kmdf-ioctlreqs.md)"><strong>IoctlReqs</strong></a></p></td>
<td align="left"><p><a href="kmdf-ioctlreqs.md" data-raw-source="[&lt;strong&gt;IoctlReqs&lt;/strong&gt;](kmdf-ioctlreqs.md)"> <strong>IoctlReqs</strong> </a>规则指定 IOCTL 请求必须不能传递给不适当 KMDF 请求或发送设备驱动程序接口 (DDIs)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-markcanconcancreqlocal.md" data-raw-source="[&lt;strong&gt;MarkCancOnCancReqLocal&lt;/strong&gt;](kmdf-markcanconcancreqlocal.md)"><strong>MarkCancOnCancReqLocal</strong></a></p></td>
<td align="left"><p><a href="kmdf-markcanconcancreqlocal.md" data-raw-source="[&lt;strong&gt;MarkCancOnCancReqLocal&lt;/strong&gt;](kmdf-markcanconcancreqlocal.md)"> <strong>MarkCancOnCancReqLocal</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable" data-raw-source="[&lt;strong&gt;WdfRequestMarkCancelable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)"> <strong>WdfRequestMarkCancelable</strong> </a>方法不能调用两个连续相同的 I/O 请求的时间。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="noioqueuepurgesynchronously.md" data-raw-source="[&lt;strong&gt;NoIoQueuePurgeSynchronously&lt;/strong&gt;](noioqueuepurgesynchronously.md)"><strong>NoIoQueuePurgeSynchronously</strong></a></p></td>
<td align="left"><p><a href="noioqueuepurgesynchronously.md" data-raw-source="[&lt;strong&gt;NoIoQueuePurgeSynchronously&lt;/strong&gt;](noioqueuepurgesynchronously.md)"> <strong>NoIoQueuePurgeSynchronously</strong> </a>规则验证 WDF 驱动程序不调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopsynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueStopSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopsynchronously)"> <strong>WdfIoQueueStopSynchronously</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrainsynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueDrainSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuedrainsynchronously)"><strong>WdfIoQueueDrainSynchronously</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueueStopAndPurgeSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestopandpurgesynchronously)"> <strong>WdfIoQueueStopAndPurgeSynchronously</strong></a>，或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurgesynchronously" data-raw-source="[&lt;strong&gt;WdfIoQueuePurgeSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuepurgesynchronously)"> <strong>WdfIoQueuePurgeSynchronously</strong> </a>函数从以下 EvtIO queue 对象事件回调函数：</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-outputbufferapi.md" data-raw-source="[&lt;strong&gt;OutputBufferAPI&lt;/strong&gt;](kmdf-outputbufferapi.md)"><strong>OutputBufferAPI</strong></a></p></td>
<td align="left"><p><a href="kmdf-outputbufferapi.md" data-raw-source="[&lt;strong&gt;OutputBufferAPI&lt;/strong&gt;](kmdf-outputbufferapi.md)"> <strong>OutputBufferAPI</strong> </a>规则指定中使用的缓冲区检索正确的 DDIs <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write" data-raw-source="[&lt;em&gt;EvtIoWrite&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)"> <em>EvtIoWrite</em> </a>回调函数。 内<em>EvtIoWrite</em>以下 DDIs 不能调用的缓冲区检索回调函数：</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-readreqs.md" data-raw-source="[&lt;strong&gt;ReadReqs&lt;/strong&gt;](kmdf-readreqs.md)"><strong>ReadReqs</strong></a></p></td>
<td align="left"><p><a href="kmdf-readreqs.md" data-raw-source="[&lt;strong&gt;ReadReqs&lt;/strong&gt;](kmdf-readreqs.md)"> <strong>ReadReqs</strong> </a>规则指定的读取请求将不传递到不适合 KMDF 方法。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-reqcompletionroutine.md" data-raw-source="[&lt;strong&gt;ReqCompletionRoutine&lt;/strong&gt;](kmdf-reqcompletionroutine.md)"><strong>ReqCompletionRoutine</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqcompletionroutine.md" data-raw-source="[&lt;strong&gt;ReqCompletionRoutine&lt;/strong&gt;](kmdf-reqcompletionroutine.md)"> <strong>ReqCompletionRoutine</strong> </a>规则指定一个请求发送到的 I/O 目标之前，必须设置完成例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-reqdelete.md" data-raw-source="[&lt;strong&gt;ReqDelete&lt;/strong&gt;](kmdf-reqdelete.md)"><strong>ReqDelete</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqdelete.md" data-raw-source="[&lt;strong&gt;ReqDelete&lt;/strong&gt;](kmdf-reqdelete.md)"> <strong>ReqDelete</strong> </a>规则指定驱动程序创建请求未传递给<em>WdfRequestCompleteXxx</em>函数。 相反，应在完成后删除的请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-reqiscanconcancreq.md" data-raw-source="[&lt;strong&gt;ReqIsCancOnCancReq&lt;/strong&gt;](kmdf-reqiscanconcancreq.md)"><strong>ReqIsCancOnCancReq</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqiscanconcancreq.md" data-raw-source="[&lt;strong&gt;ReqIsCancOnCancReq&lt;/strong&gt;](kmdf-reqiscanconcancreq.md)"> <strong>ReqIsCancOnCancReq</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestiscanceled" data-raw-source="[&lt;strong&gt;WdfRequestIsCanceled&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestiscanceled)"> <strong>WdfRequestIsCanceled</strong> </a>只有不是一个请求上调用方法标记为可取消。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-reqmarkcancelablesend.md" data-raw-source="[&lt;strong&gt;ReqMarkCancelableSend&lt;/strong&gt;](kmdf-reqmarkcancelablesend.md)"><strong>ReqMarkCancelableSend</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqmarkcancelablesend.md" data-raw-source="[&lt;strong&gt;ReqMarkCancelableSend&lt;/strong&gt;](kmdf-reqmarkcancelablesend.md)"> <strong>ReqMarkCancelableSend</strong> </a>规则指定的驱动程序转发的请求未标记为可取消通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable" data-raw-source="[&lt;strong&gt;WdfRequestMarkCancelable&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)"> <strong>WdfRequestMarkCancelable</strong></a>.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-requestcompleted.md" data-raw-source="[&lt;strong&gt;RequestCompleted&lt;/strong&gt;](kmdf-requestcompleted.md)"><strong>RequestCompleted</strong></a></p></td>
<td align="left"><p><a href="kmdf-deferredrequestcompleted.md" data-raw-source="[&lt;strong&gt;DeferredRequestCompleted&lt;/strong&gt;](kmdf-deferredrequestcompleted.md)"> <strong>DeferredRequestCompleted</strong> </a>规则指定，对于非筛选器驱动程序提供给驱动程序的默认 I/O 队列的每个请求必须完成，除非请求延迟或转发，或如果<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge" data-raw-source="[&lt;strong&gt;WdfRequestStopAcknowledge&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)"> <strong>WdfRequestStopAcknowledge</strong> </a>调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-requestformattedvalid.md" data-raw-source="[&lt;strong&gt;RequestFormattedValid&lt;/strong&gt;](kmdf-requestformattedvalid.md)"><strong>RequestFormattedValid</strong></a></p></td>
<td align="left"><p><a href="kmdf-requestformattedvalid.md" data-raw-source="[&lt;strong&gt;RequestFormattedValid&lt;/strong&gt;](kmdf-requestformattedvalid.md)"> <strong>RequestFormattedValid</strong> </a>规则指定驱动程序格式所有请求，但 WDF_REQUEST_SEND_OPTION_SEND_AND_FORGET 请求除外，它将它们发送到的 I/O 目标之前。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-requestgetstatusvalid.md" data-raw-source="[&lt;strong&gt;RequestGetStatusValid&lt;/strong&gt;](kmdf-requestgetstatusvalid.md)"><strong>RequestGetStatusValid</strong></a></p></td>
<td align="left"><p><a href="kmdf-requestgetstatusvalid.md" data-raw-source="[&lt;strong&gt;RequestGetStatusValid&lt;/strong&gt;](kmdf-requestgetstatusvalid.md)"> <strong>RequestGetStatusValid</strong> </a>规则，规定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetstatus" data-raw-source="[&lt;strong&gt;WdfRequestGetStatus&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetstatus)"> <strong>WdfRequestGetStatus</strong> </a>应中的一个请求的调用以下情况：</p>
<ul>
<li>当<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)"> <strong>WdfRequestSend</strong> </a>返回失败。</li>
<li>当请求已发送与 WDF_REQUEST_SEND_OPTION_SYNCHRONOUS。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-requestsendandforgetnoformatting.md" data-raw-source="[&lt;strong&gt;RequestSendAndForgetNoFormatting&lt;/strong&gt;](kmdf-requestsendandforgetnoformatting.md)"><strong>RequestSendAndForgetNoFormatting</strong></a></p></td>
<td align="left"><p><a href="kmdf-requestsendandforgetnoformatting.md" data-raw-source="[&lt;strong&gt;RequestSendAndForgetNoFormatting&lt;/strong&gt;](kmdf-requestsendandforgetnoformatting.md)"> <strong>RequestSendAndForgetNoFormatting</strong> </a>规则验证该驱动程序不会格式化 I/O 目标格式设置函数中将其发送到发送选项 WDF_ I/O 目标之前使用的请求REQUEST_SEND_OPTION_SEND_AND_FORGET。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-requestsendandforgetnoformatting2.md" data-raw-source="[&lt;strong&gt;RequestSendAndForgetNoFormatting2&lt;/strong&gt;](kmdf-requestsendandforgetnoformatting2.md)"><strong>RequestSendAndForgetNoFormatting2</strong></a></p></td>
<td align="left"><p><a href="kmdf-requestsendandforgetnoformatting2.md" data-raw-source="[&lt;strong&gt;RequestSendAndForgetNoFormatting2&lt;/strong&gt;](kmdf-requestsendandforgetnoformatting2.md)"> <strong>RequestSendAndForgetNoFormatting2</strong> </a>规则验证该驱动程序不会格式化 I/O 目标格式设置函数中将其发送到发送选项 WDF_ I/O 目标之前使用的请求REQUEST_SEND_OPTION_SEND_AND_FORGET。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-stopackwithinevtiostop.md" data-raw-source="[&lt;strong&gt;StopAckWithinEvtIoStop&lt;/strong&gt;](kmdf-stopackwithinevtiostop.md)"><strong>StopAckWithinEvtIoStop</strong></a></p></td>
<td align="left"><p><a href="kmdf-stopackwithinevtiostop.md" data-raw-source="[&lt;strong&gt;StopAckWithinEvtIoStop&lt;/strong&gt;](kmdf-stopackwithinevtiostop.md)"> <strong>StopAckWithinEvtIoStop</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge" data-raw-source="[&lt;strong&gt;WdfRequestStopAcknowledge&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)"> <strong>WdfRequestStopAcknowledge</strong> </a>内仅调用函数<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"> <em>EvtIoStop</em> </a>回调函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfioqueuefindrequestfailed.md" data-raw-source="[&lt;strong&gt;WdfIoQueueFindRequestFailed&lt;/strong&gt;](kmdf-wdfioqueuefindrequestfailed.md)"><strong>WdfIoQueueFindRequestFailed</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfioqueuefindrequestfailed.md" data-raw-source="[&lt;strong&gt;WdfIoQueueFindRequestFailed&lt;/strong&gt;](kmdf-wdfioqueuefindrequestfailed.md)"> <strong>WdfIoQueueFindRequestFailed</strong> </a>规则指定<a href="kmdf-wdfioqueueretrievefoundrequest.md" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveFoundRequest&lt;/strong&gt;](kmdf-wdfioqueueretrievefoundrequest.md)"> <strong>WdfIoQueueRetrieveFoundRequest</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference" data-raw-source="[&lt;strong&gt;WdfObjectDereference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)"> <strong>WdfObjectDereference</strong> </a>应该只能在调用<strong>WdfIoQueueFindRequestFailed</strong>返回 STATUS_SUCCESS。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-wdfioqueueretrievefoundrequest.md" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveFoundRequest&lt;/strong&gt;](kmdf-wdfioqueueretrievefoundrequest.md)"><strong>WdfIoQueueRetrieveFoundRequest</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfioqueueretrievefoundrequest.md" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveFoundRequest&lt;/strong&gt;](kmdf-wdfioqueueretrievefoundrequest.md)"> <strong>WdfIoQueueRetrieveFoundRequest</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveFoundRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest)"> <strong>WdfIoQueueRetrieveFoundRequest</strong> </a>后，才调用方法<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuefindrequest" data-raw-source="[&lt;strong&gt;WdfIoQueueFindRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuefindrequest)"> <strong>WdfIoQueueFindRequest</strong> </a>调用并返回 STATUS_SUCCESS，但不<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference" data-raw-source="[&lt;strong&gt;WdfObjectDereference&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfobjectdereference)"> <strong>WdfObjectDereference</strong> </a>上调用同一请求中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfioqueueretrievenextrequest.md" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveNextRequest&lt;/strong&gt;](kmdf-wdfioqueueretrievenextrequest.md)"><strong>WdfIoQueueRetrieveNextRequest</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfioqueueretrievenextrequest.md" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveNextRequest&lt;/strong&gt;](kmdf-wdfioqueueretrievenextrequest.md)"> <strong>WdfIoQueueRetrieveNextRequest</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueretrievenextrequest" data-raw-source="[&lt;strong&gt;WdfIoQueueRetrieveNextRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueueretrievenextrequest)"> <strong>WdfIoQueueRetrieveNextRequest</strong> </a> 后未调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuefindrequest" data-raw-source="[&lt;strong&gt;WdfIoQueueFindRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuefindrequest)"><strong>WdfIoQueueFindRequest</strong> </a>调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-writereqs.md" data-raw-source="[&lt;strong&gt;WriteReqs&lt;/strong&gt;](kmdf-writereqs.md)"><strong>WriteReqs</strong></a></p></td>
<td align="left"><p><a href="kmdf-writereqs.md" data-raw-source="[&lt;strong&gt;WriteReqs&lt;/strong&gt;](kmdf-writereqs.md)"> <strong>WriteReqs</strong> </a>规则指定写入请求不会传递到不适合 KMDF 方法。</p></td>
</tr>
</tbody>
</table>

 

**若要选择 RequestProcessing 规则集**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...** .

2.  单击**规则**选项卡。下**规则集**，选择**RequestProcessing**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**RequestProcessing.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:RequestProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)并[Static Driver Verifier 命令 (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 





