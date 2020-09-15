---
title: IrpProcessing 规则集 (WDM)
description: 使用这些规则验证你的驱动程序是否正确处理 (IRP) 的 i/o 请求包。
ms.assetid: C11F1FD7-DA41-4A72-A0EB-97C1D79ECC21
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2b508522eb88ddcc7e2d35a34f73fcca5bebd08b
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105316"
---
# <a name="irpprocessing-rule-set-wdm"></a>IrpProcessing 规则集 (WDM)


使用这些规则验证你的驱动程序是否正确处理 (IRP) 的 i/o 请求包。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="wdm-completerequest.md" data-raw-source="[&lt;strong&gt;CompleteRequest&lt;/strong&gt;](wdm-completerequest.md)"><strong>CompleteRequest</strong></a></p></td>
<td align="left"><p><a href="wdm-completerequest.md" data-raw-source="[&lt;strong&gt;CompleteRequest&lt;/strong&gt;](wdm-completerequest.md)"><strong>CompleteRequest</strong></a>规则验证在完成例程运行后不调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a>例程，并且它不会返回 STATUS_MORE_PROCESSING_REQUIRED。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-completerequeststatuscheck.md" data-raw-source="[&lt;strong&gt;CompleteRequestStatusCheck&lt;/strong&gt;](wdm-completerequeststatuscheck.md)"><strong>CompleteRequestStatusCheck</strong></a></p></td>
<td align="left"><p><a href="wdm-completerequeststatuscheck.md" data-raw-source="[&lt;strong&gt;CompleteRequestStatusCheck&lt;/strong&gt;](wdm-completerequeststatuscheck.md)"><strong>CompleteRequestStatusCheck</strong></a>规则验证 IRP 中的 i/o 状态值是否与下部驱动程序返回的状态值匹配。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-completionroutineregistered.md" data-raw-source="[&lt;strong&gt;CompletionRoutineRegistered&lt;/strong&gt;](wdm-completionroutineregistered.md)"><strong>CompletionRoutineRegistered</strong></a></p></td>
<td align="left"><p><a href="wdm-completionroutineregistered.md" data-raw-source="[&lt;strong&gt;CompletionRoutineRegistered&lt;/strong&gt;](wdm-completionroutineregistered.md)"><strong>CompletionRoutineRegistered</strong></a>规则指定如果调度例程使用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)"><strong>IoSetCompletionRoutineEx</strong></a>注册了<a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;strong&gt;IoCompletion&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)"><strong>IoCompletion</strong></a>例程，则调度例程之后必须调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>或<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>PoCallDriver</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-doublecompletion.md" data-raw-source="[&lt;strong&gt;DoubleCompletion&lt;/strong&gt;](wdm-doublecompletion.md)"><strong>DoubleCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-doublecompletion.md" data-raw-source="[&lt;strong&gt;DoubleCompletion (WDM)&lt;/strong&gt;](wdm-doublecompletion.md)"><strong>DoubleCompletion (WDM) </strong></a>规则指定驱动程序不得为同一 IRP 调用两次<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a>例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-ioreuseirp.md" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](wdm-ioreuseirp.md)"><strong>IoReuseIrp</strong></a></p></td>
<td align="left"><p><a href="wdm-ioreuseirp.md" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](wdm-ioreuseirp.md)"><strong>IoReuseIrp</strong></a>规则指定，驱动程序只应在以前使用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)"><strong>IoAllocateIrp</strong></a>分配的 irp 上使用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp)"><strong>IoReuseIrp</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-ioreuseirp2.md" data-raw-source="[&lt;strong&gt;IoReuseIrp2&lt;/strong&gt;](wdm-ioreuseirp2.md)"><strong>IoReuseIrp2</strong></a></p></td>
<td align="left"><p><a href="wdm-ioreuseirp2.md" data-raw-source="[&lt;strong&gt;IoReuseIrp2&lt;/strong&gt;](wdm-ioreuseirp2.md)"><strong>IoReuseIrp2</strong></a>规则指定，驱动程序应仅对先前在驱动程序中分配的 Irp 使用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp)"><strong>IoReuseIrp</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iosetcompletionexcompleteirp.md" data-raw-source="[&lt;strong&gt;IoSetCompletionExCompleteIrp&lt;/strong&gt;](wdm-iosetcompletionexcompleteirp.md)"><strong>IoSetCompletionExCompleteIrp</strong></a></p></td>
<td align="left"><p><a href="wdm-iosetcompletionexcompleteirp.md" data-raw-source="[&lt;strong&gt;IoSetCompletionExCompleteIrp&lt;/strong&gt;](wdm-iosetcompletionexcompleteirp.md)"><strong>IoSetCompletionExCompleteIrp</strong></a>规则指定<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)"><strong>IoSetCompletionRoutineEx</strong></a>例程返回一个 NTSTATUS 值。 驱动程序必须检查此值以确定在调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>或<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>PoCallDriver</strong></a>之前是否已成功注册<a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)"><em>IoCompletion</em></a>例程，如果<strong>IoSetCompletionRoutineEx</strong>失败，则应完成 IRP 并返回调度例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iosetcompletionroutineexcheck.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineExCheck&lt;/strong&gt;](wdm-iosetcompletionroutineexcheck.md)"><strong>IoSetCompletionRoutineExCheck</strong></a></p></td>
<td align="left"><p><a href="wdm-iosetcompletionroutineexcheck.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineExCheck&lt;/strong&gt;](wdm-iosetcompletionroutineexcheck.md)"><strong>IoSetCompletionRoutineExCheck</strong></a>规则指定<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)"><strong>IoSetCompletionRoutineEx</strong></a>例程返回一个 NTSTATUS 值。 驱动程序必须选中此值，以确定是否已成功注册 <a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)"><em>IoCompletion</em></a> 例程，然后再调用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a> 或 <a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>PoCallDriver</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iosetcompletionroutineexcheckdeviceobject.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineExCheckDeviceObject&lt;/strong&gt;](wdm-iosetcompletionroutineexcheckdeviceobject.md)"><strong>IoSetCompletionRoutineExCheckDeviceObject</strong></a></p></td>
<td align="left"><p><a href="wdm-iosetcompletionroutineexcheckdeviceobject.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineExCheckDeviceObject&lt;/strong&gt;](wdm-iosetcompletionroutineexcheckdeviceobject.md)"><strong>IoSetCompletionRoutineExCheckDeviceObject</strong></a>规则指定，如果当前设备对象未传递到<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)"><strong>IoSetCompletionRoutineEx</strong></a> ，而较低的设备对象为，则可能会导致争用条件，即使完成例程尚未运行，也可以卸载当前设备对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iosetcompletionroutinenonpnpdriver.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineNonPnpDriver&lt;/strong&gt;](wdm-iosetcompletionroutinenonpnpdriver.md)"><strong>IoSetCompletionRoutineNonPnpDriver</strong></a></p></td>
<td align="left"><p><a href="wdm-iosetcompletionroutinenonpnpdriver.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineNonPnpDriver&lt;/strong&gt;](wdm-iosetcompletionroutinenonpnpdriver.md)"><strong>IoSetCompletionRoutineNonPnpDriver</strong></a>规则指定非 PnP 驱动程序的驱动程序应使用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)"><strong>IoSetCompletionRoutineEx</strong></a> not <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutine&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)"><strong>IoSetCompletionRoutine</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irpcancelfield.md" data-raw-source="[&lt;strong&gt;IrpCancelField&lt;/strong&gt;](wdm-irpcancelfield.md)"><strong>IrpCancelField</strong></a></p></td>
<td align="left"><p><a href="wdm-irpcancelfield.md" data-raw-source="[&lt;strong&gt;IrpCancelField&lt;/strong&gt;](wdm-irpcancelfield.md)"><strong>IrpCancelField</strong></a>规则指定该驱动程序在其挂起的 Irp 上设置取消例程时，检查<strong>irp- &gt; Cancel</strong>成员的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irpprocessingcomplete.md" data-raw-source="[&lt;strong&gt;IrpProcessingComplete&lt;/strong&gt;](wdm-irpprocessingcomplete.md)"><strong>IrpProcessingComplete</strong></a></p></td>
<td align="left"><p><a href="wdm-irpprocessingcomplete.md" data-raw-source="[&lt;strong&gt;IrpProcessingComplete&lt;/strong&gt;](wdm-irpprocessingcomplete.md)"><strong>IrpProcessingComplete</strong></a>规则指定如果派单例程返回 STATUS_SUCCESS，则 IRP 必须已由驱动程序本身或较低级别的驱动程序完成。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-lowerdriverreturn.md" data-raw-source="[&lt;strong&gt;LowerDriverReturn&lt;/strong&gt;](wdm-lowerdriverreturn.md)"><strong>LowerDriverReturn</strong></a></p></td>
<td align="left"><p><a href="wdm-lowerdriverreturn.md" data-raw-source="[&lt;strong&gt;LowerDriverReturn&lt;/strong&gt;](wdm-lowerdriverreturn.md)"><strong>LowerDriverReturn</strong></a>规则指定在使用<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>PoCallDriver</strong></a>或<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>调用较低的驱动程序后，该驱动程序将从调用中保存返回状态，并将接收到的返回状态传递到调度例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-signaleventincompletion.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion&lt;/strong&gt;](wdm-signaleventincompletion.md)"><strong>SignalEventInCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-signaleventincompletion.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion&lt;/strong&gt;](wdm-signaleventincompletion.md)"><strong>SignalEventInCompletion</strong></a>规则指定在处理异步 IRP 时，如果设置了<strong>IRP- &gt; PendingReturned</strong>标志，驱动程序需要在完成例程中调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-signaleventincompletion2.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion2&lt;/strong&gt;](wdm-signaleventincompletion2.md)"><strong>SignalEventInCompletion2</strong></a></p></td>
<td align="left"><p><a href="wdm-signaleventincompletion2.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion2&lt;/strong&gt;](wdm-signaleventincompletion2.md)"><strong>SignalEventInCompletion2</strong></a>规则指定在处理异步 IRP 时，如果设置了<strong>IRP- &gt; PendingReturned</strong>标志，驱动程序需要在完成例程中调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-signaleventincompletion3.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion3&lt;/strong&gt;](wdm-signaleventincompletion3.md)"><strong>SignalEventInCompletion3</strong></a></p></td>
<td align="left"><p><a href="wdm-signaleventincompletion3.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion3&lt;/strong&gt;](wdm-signaleventincompletion3.md)"><strong>SignalEventInCompletion3</strong></a>规则指定在处理异步 IRP 时，如果设置了<strong>IRP- &gt; PendingReturned</strong>标志，驱动程序需要在完成例程中调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-startiocancel.md" data-raw-source="[&lt;strong&gt;StartIoCancel&lt;/strong&gt;](wdm-startiocancel.md)"><strong>StartIoCancel</strong></a></p></td>
<td align="left"><p><a href="wdm-startiocancel.md" data-raw-source="[&lt;strong&gt;StartIoCancel&lt;/strong&gt;](wdm-startiocancel.md)"><strong>StartIoCancel</strong></a>规则指定，在使用非<strong>NULL</strong><a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel" data-raw-source="[&lt;strong&gt;Cancel&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)"><strong>Cancel</strong></a>例程调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine" data-raw-source="[&lt;strong&gt;IoSetCancelRoutine&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)"><strong>IoSetCancelRoutine</strong></a>之前，驱动程序不得调用<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes" data-raw-source="[&lt;strong&gt;IoSetStartIoAttributes&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes)"><strong>IoSetStartIoAttributes</strong></a> ，并将<em>NonCancelable</em>参数设置为<strong>FALSE</strong> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-startiorecursion.md" data-raw-source="[&lt;strong&gt;StartIoRecursion&lt;/strong&gt;](wdm-startiorecursion.md)"><strong>StartIoRecursion</strong></a></p></td>
<td align="left"><p><a href="wdm-startiorecursion.md" data-raw-source="[&lt;strong&gt;StartIoRecursion&lt;/strong&gt;](wdm-startiorecursion.md)"><strong>StartIoRecursion</strong></a>规则指定如果驱动程序的<a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio" data-raw-source="[&lt;strong&gt;StartIo&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)"><strong>StartIo</strong></a>例程包括对<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket" data-raw-source="[&lt;strong&gt;IoStartNextPacket&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)"><strong>IoStartNextPacket</strong></a>的调用，则驱动程序必须先调用<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes" data-raw-source="[&lt;strong&gt;IoSetStartIoAttributes&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes)"><strong>IoSetStartIoAttributes</strong></a> ，并将<em>DeferredStartIo</em>属性设置为<strong>TRUE</strong>。 否则，可能会导致无限递归。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pnpremove.md" data-raw-source="[&lt;strong&gt;PnpRemove&lt;/strong&gt;](wdm-pnpremove.md)"><strong>PnpRemove</strong></a></p></td>
<td align="left"><p><a href="wdm-pnpremove.md" data-raw-source="[&lt;strong&gt;PnpRemove&lt;/strong&gt;](wdm-pnpremove.md)"><strong>PnpRemove</strong></a>规则指定驱动程序无法 IRP_MN_CANCEL_REMOVE_DEVICE、IRP_MN_CANCEL_STOP_DEVICE 或 IRP_MN_REMOVE_DEVICE 请求中 IRP_MN_SURPRISE_REMOVAL 完成失败的请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-pnpsurpriseremove.md" data-raw-source="[&lt;strong&gt;PnpSurpriseRemove&lt;/strong&gt;](wdm-pnpsurpriseremove.md)"><strong>PnpSurpriseRemove</strong></a></p></td>
<td align="left"><p><a href="wdm-pnpsurpriseremove.md" data-raw-source="[&lt;strong&gt;PnpSurpriseRemove&lt;/strong&gt;](wdm-pnpsurpriseremove.md)"><strong>PnpSurpriseRemove</strong></a>规则指定在处理<a href="/windows-hardware/drivers/kernel/irp-mn-surprise-removal" data-raw-source="[&lt;strong&gt;IRP_MN_SURPRISE_REMOVAL&lt;/strong&gt;](../kernel/irp-mn-surprise-removal.md)"><strong>IRP_MN_SURPRISE_REMOVAL</strong></a>请求时，驱动程序不调用 IoDeleteDevice 或 IoDetachDevice。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-powerdownallocate.md" data-raw-source="[&lt;strong&gt;PowerDownAllocate&lt;/strong&gt;](wdm-powerdownallocate.md)"><strong>PowerDownAllocate</strong></a></p></td>
<td align="left"><p><a href="wdm-powerdownallocate.md" data-raw-source="[&lt;strong&gt;PowerDownAllocate&lt;/strong&gt;](wdm-powerdownallocate.md)"><strong>PowerDownAllocate</strong></a>规则指定在处理从 s0 到 [S1 ... 的<strong>SystemPowerState</strong>转换的 IRP_MN_SET_POWER 请求时，FDO 和 FIDO 驱动程序不应分配内存。S5]。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-powerdownfail.md" data-raw-source="[&lt;strong&gt;PowerDownFail&lt;/strong&gt;](wdm-powerdownfail.md)"><strong>PowerDownFail</strong></a></p></td>
<td align="left"><p><a href="wdm-powerdownfail.md" data-raw-source="[&lt;strong&gt;PowerDownFail&lt;/strong&gt;](wdm-powerdownfail.md)"><strong>PowerDownFail</strong></a>规则指定在设备关机时，FDO 或 FIDO 驱动程序不应 IRP_MN_SET_POWER 请求失败。 此规则仅适用于 FDO 和 FIDO 驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-powerirpddis.md" data-raw-source="[&lt;strong&gt;PowerIrpDDIs&lt;/strong&gt;](wdm-powerirpddis.md)"><strong>PowerIrpDDIs</strong></a></p></td>
<td align="left"><p><a href="wdm-powerirpddis.md" data-raw-source="[&lt;strong&gt;PowerIrpDDIs&lt;/strong&gt;](wdm-powerirpddis.md)"><strong>PowerIrpDDIs</strong></a>规则指定当驱动程序使用 IRP_MN_SET_POWER 处理系统或设备 IRP_MJ_POWER 时，它不应调用只能在 PASSIVE_LEVEL 调用的 DDIs。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-powerupfail.md" data-raw-source="[&lt;strong&gt;PowerUpFail&lt;/strong&gt;](wdm-powerupfail.md)"><strong>PowerUpFail</strong></a></p></td>
<td align="left"><p>PowerUpFail 规则指定在设备打开时，FDO 或 FIDO 驱动程序不应将 IRP_MN_SET_POWER 请求失败。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pnpirpcompletion.md" data-raw-source="[&lt;strong&gt;PnpIrpCompletion&lt;/strong&gt;](wdm-pnpirpcompletion.md)"><strong>PnpIrpCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-pnpirpcompletion.md" data-raw-source="[&lt;strong&gt;PnpIrpCompletion&lt;/strong&gt;](wdm-pnpirpcompletion.md)"><strong>PnpIrpCompletion</strong></a>规则验证 FDO 驱动程序是否将 PnP irp 传递到低级驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-wmicomplete.md" data-raw-source="[&lt;strong&gt;WmiComplete&lt;/strong&gt;](wdm-wmicomplete.md)"><strong>WmiComplete</strong></a></p></td>
<td align="left"><p><a href="wdm-wmicomplete.md" data-raw-source="[&lt;strong&gt;WmiComplete&lt;/strong&gt;](wdm-wmicomplete.md)"><strong>WmiComplete</strong></a>规则指定在处理<a href="/windows-hardware/drivers/kernel/wmi-minor-irps" data-raw-source="[&lt;strong&gt;WMI minor IRP&lt;/strong&gt;](../kernel/wmi-minor-irps.md)"><strong>WMI 次要 IRP</strong></a>时，驱动程序会在从<a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;strong&gt;DispatchSystemControl&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><strong>DispatchSystemControl</strong></a>例程返回之前调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-wmiforward.md" data-raw-source="[&lt;strong&gt;WmiForward&lt;/strong&gt;](wdm-wmiforward.md)"><strong>WmiForward</strong></a></p></td>
<td align="left"><p><a href="wdm-wmiforward.md" data-raw-source="[&lt;strong&gt;WmiForward&lt;/strong&gt;](wdm-wmiforward.md)"><strong>WmiForward</strong></a>规则指定当需要转发时，驱动程序必须转发<a href="/windows-hardware/drivers/kernel/wmi-minor-irps" data-raw-source="[&lt;strong&gt;WMI minor IRPs&lt;/strong&gt;](../kernel/wmi-minor-irps.md)"><strong>WMI 次要 irp</strong></a> 。</p></td>
</tr>
</tbody>
</table>

 

**选择 IrpProcessing 规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 **IrpProcessing**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**IrpProcessing。 sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:IrpProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

