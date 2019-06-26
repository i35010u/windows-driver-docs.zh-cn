---
title: IrpProcessing 规则集 (WDM)
description: 使用这些规则来验证您的驱动程序正确处理 I/O 请求数据包 (IRP)。
ms.assetid: C11F1FD7-DA41-4A72-A0EB-97C1D79ECC21
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 06a4dfc4288edcbba7edeeec90b4c6fdc2f2329d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373683"
---
# <a name="irpprocessing-rule-set-wdm"></a>IrpProcessing 规则集 (WDM)


使用这些规则来验证您的驱动程序正确处理 I/O 请求数据包 (IRP)。

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
<td align="left"><p><a href="wdm-completerequest.md" data-raw-source="[&lt;strong&gt;CompleteRequest&lt;/strong&gt;](wdm-completerequest.md)"><strong>CompleteRequest</strong></a></p></td>
<td align="left"><p><a href="wdm-completerequest.md" data-raw-source="[&lt;strong&gt;CompleteRequest&lt;/strong&gt;](wdm-completerequest.md)"> <strong>CompleteRequest</strong> </a>规则验证<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)"> <strong>IoCompleteRequest</strong> </a>完成例程运行后，不调用例程和它不返回 STATUS_MORE_PROCESSING_REQUIRED。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-completerequeststatuscheck.md" data-raw-source="[&lt;strong&gt;CompleteRequestStatusCheck&lt;/strong&gt;](wdm-completerequeststatuscheck.md)"><strong>CompleteRequestStatusCheck</strong></a></p></td>
<td align="left"><p><a href="wdm-completerequeststatuscheck.md" data-raw-source="[&lt;strong&gt;CompleteRequestStatusCheck&lt;/strong&gt;](wdm-completerequeststatuscheck.md)"> <strong>CompleteRequestStatusCheck</strong> </a>规则验证是否在 IRP 的 I/O 状态值匹配较低的驱动程序返回的状态值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-completionroutineregistered.md" data-raw-source="[&lt;strong&gt;CompletionRoutineRegistered&lt;/strong&gt;](wdm-completionroutineregistered.md)"><strong>CompletionRoutineRegistered</strong></a></p></td>
<td align="left"><p><a href="wdm-completionroutineregistered.md" data-raw-source="[&lt;strong&gt;CompletionRoutineRegistered&lt;/strong&gt;](wdm-completionroutineregistered.md)"> <strong>CompletionRoutineRegistered</strong> </a>规则指定，如果调度例程寄存器<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;strong&gt;IoCompletion&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)"> <strong>IoCompletion</strong> </a>例程，并使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex)"> <strong>IoSetCompletionRoutineEx</strong></a>，此后必须调用的调度例程<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"> <strong>IoCallDriver</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"> <strong>PoCallDriver</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-doublecompletion.md" data-raw-source="[&lt;strong&gt;DoubleCompletion&lt;/strong&gt;](wdm-doublecompletion.md)"><strong>DoubleCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-doublecompletion.md" data-raw-source="[&lt;strong&gt;DoubleCompletion (WDM)&lt;/strong&gt;](wdm-doublecompletion.md)"> <strong>DoubleCompletion (WDM)</strong> </a>规则指定驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)"> <strong>IoCompleteRequest</strong> </a>两次的相同例程IRP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-ioreuseirp.md" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](wdm-ioreuseirp.md)"><strong>IoReuseIrp</strong></a></p></td>
<td align="left"><p><a href="wdm-ioreuseirp.md" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](wdm-ioreuseirp.md)"> <strong>IoReuseIrp</strong> </a>规则指定一个驱动程序应使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreuseirp" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreuseirp)"> <strong>IoReuseIrp</strong> </a>仅在它与以前分配的Irp<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)"><strong>IoAllocateIrp</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-ioreuseirp2.md" data-raw-source="[&lt;strong&gt;IoReuseIrp2&lt;/strong&gt;](wdm-ioreuseirp2.md)"><strong>IoReuseIrp2</strong></a></p></td>
<td align="left"><p><a href="wdm-ioreuseirp2.md" data-raw-source="[&lt;strong&gt;IoReuseIrp2&lt;/strong&gt;](wdm-ioreuseirp2.md)"> <strong>IoReuseIrp2</strong> </a>规则指定一个驱动程序应使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreuseirp" data-raw-source="[&lt;strong&gt;IoReuseIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreuseirp)"> <strong>IoReuseIrp</strong> </a>仅在它以前在内部分配的 Irp驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iosetcompletionexcompleteirp.md" data-raw-source="[&lt;strong&gt;IoSetCompletionExCompleteIrp&lt;/strong&gt;](wdm-iosetcompletionexcompleteirp.md)"><strong>IoSetCompletionExCompleteIrp</strong></a></p></td>
<td align="left"><p><a href="wdm-iosetcompletionexcompleteirp.md" data-raw-source="[&lt;strong&gt;IoSetCompletionExCompleteIrp&lt;/strong&gt;](wdm-iosetcompletionexcompleteirp.md)"> <strong>IoSetCompletionExCompleteIrp</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex)"> <strong>IoSetCompletionRoutineEx</strong> </a>例程将返回 NTSTATUS 值. 该驱动程序必须检查此值可确定是否<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)"> <em>IoCompletion</em> </a>例程已成功注册，然后再调<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"> <strong>IoCallDriver</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"> <strong>PoCallDriver</strong> </a>如果<strong>IoSetCompletionRoutineEx</strong>失败，则应完成 IRP，并应返回的调度例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iosetcompletionroutineexcheck.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineExCheck&lt;/strong&gt;](wdm-iosetcompletionroutineexcheck.md)"><strong>IoSetCompletionRoutineExCheck</strong></a></p></td>
<td align="left"><p><a href="wdm-iosetcompletionroutineexcheck.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineExCheck&lt;/strong&gt;](wdm-iosetcompletionroutineexcheck.md)"> <strong>IoSetCompletionRoutineExCheck</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex)"> <strong>IoSetCompletionRoutineEx</strong> </a>例程将返回 NTSTATUS值。 该驱动程序必须检查此值可确定是否<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)"> <em>IoCompletion</em> </a>例程已成功注册，然后再调<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"> <strong>IoCallDriver</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"> <strong>PoCallDriver</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iosetcompletionroutineexcheckdeviceobject.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineExCheckDeviceObject&lt;/strong&gt;](wdm-iosetcompletionroutineexcheckdeviceobject.md)"><strong>IoSetCompletionRoutineExCheckDeviceObject</strong></a></p></td>
<td align="left"><p><a href="wdm-iosetcompletionroutineexcheckdeviceobject.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineExCheckDeviceObject&lt;/strong&gt;](wdm-iosetcompletionroutineexcheckdeviceobject.md)"> <strong>IoSetCompletionRoutineExCheckDeviceObject</strong> </a>规则指定如果当前的设备对象不传递给<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex)"> <strong>IoSetCompletionRoutineEx</strong></a>和较低的设备对象是，这可能会导致争用条件其中当前的设备对象的可卸载即使尚未运行完成例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iosetcompletionroutinenonpnpdriver.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineNonPnpDriver&lt;/strong&gt;](wdm-iosetcompletionroutinenonpnpdriver.md)"><strong>IoSetCompletionRoutineNonPnpDriver</strong></a></p></td>
<td align="left"><p><a href="wdm-iosetcompletionroutinenonpnpdriver.md" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineNonPnpDriver&lt;/strong&gt;](wdm-iosetcompletionroutinenonpnpdriver.md)"> <strong>IoSetCompletionRoutineNonPnpDriver</strong> </a>规则指定驱动程序不是即插即用驱动程序应使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutineEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex)"> <strong>IoSetCompletionRoutineEx</strong> </a>不<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine" data-raw-source="[&lt;strong&gt;IoSetCompletionRoutine&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)"> <strong>IoSetCompletionRoutine</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irpcancelfield.md" data-raw-source="[&lt;strong&gt;IrpCancelField&lt;/strong&gt;](wdm-irpcancelfield.md)"><strong>IrpCancelField</strong></a></p></td>
<td align="left"><p><a href="wdm-irpcancelfield.md" data-raw-source="[&lt;strong&gt;IrpCancelField&lt;/strong&gt;](wdm-irpcancelfield.md)"> <strong>IrpCancelField</strong> </a>规则指定驱动程序检查的值<strong>Irp-&gt;取消</strong>它具有成员在 IRP 设置在取消例程时挂起。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irpprocessingcomplete.md" data-raw-source="[&lt;strong&gt;IrpProcessingComplete&lt;/strong&gt;](wdm-irpprocessingcomplete.md)"><strong>IrpProcessingComplete</strong></a></p></td>
<td align="left"><p><a href="wdm-irpprocessingcomplete.md" data-raw-source="[&lt;strong&gt;IrpProcessingComplete&lt;/strong&gt;](wdm-irpprocessingcomplete.md)"> <strong>IrpProcessingComplete</strong> </a>规则指定是否在调度例程返回 STATUS_SUCCESS，是否 IRP 必须已完成任一驱动程序本身或较低级别驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-lowerdriverreturn.md" data-raw-source="[&lt;strong&gt;LowerDriverReturn&lt;/strong&gt;](wdm-lowerdriverreturn.md)"><strong>LowerDriverReturn</strong></a></p></td>
<td align="left"><p><a href="wdm-lowerdriverreturn.md" data-raw-source="[&lt;strong&gt;LowerDriverReturn&lt;/strong&gt;](wdm-lowerdriverreturn.md)"> <strong>LowerDriverReturn</strong> </a>规则指定后使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"> <strong>PoCallDriver</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"> <strong>IoCallDriver</strong> </a>若要调用的较低的驱动程序，该驱动程序将返回状态保存从调用，并将它收到的返回状态传递到调度例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-signaleventincompletion.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion&lt;/strong&gt;](wdm-signaleventincompletion.md)"><strong>SignalEventInCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-signaleventincompletion.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion&lt;/strong&gt;](wdm-signaleventincompletion.md)"> <strong>SignalEventInCompletion</strong> </a>规则指定在处理异步 IRP，该驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)"> <strong>KeSetEvent</strong> </a>中完成例程时<strong>Irp-&gt;PendingReturned</strong>设置标志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-signaleventincompletion2.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion2&lt;/strong&gt;](wdm-signaleventincompletion2.md)"><strong>SignalEventInCompletion2</strong></a></p></td>
<td align="left"><p><a href="wdm-signaleventincompletion2.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion2&lt;/strong&gt;](wdm-signaleventincompletion2.md)"> <strong>SignalEventInCompletion2</strong> </a>规则指定在处理异步 IRP，该驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)"> <strong>KeSetEvent</strong> </a>中完成例程时<strong>Irp-&gt;PendingReturned</strong>设置标志。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-signaleventincompletion3.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion3&lt;/strong&gt;](wdm-signaleventincompletion3.md)"><strong>SignalEventInCompletion3</strong></a></p></td>
<td align="left"><p><a href="wdm-signaleventincompletion3.md" data-raw-source="[&lt;strong&gt;SignalEventInCompletion3&lt;/strong&gt;](wdm-signaleventincompletion3.md)"> <strong>SignalEventInCompletion3</strong> </a>规则指定在处理异步 IRP，该驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)"> <strong>KeSetEvent</strong> </a>中完成例程时<strong>Irp-&gt;PendingReturned</strong>设置标志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-startiocancel.md" data-raw-source="[&lt;strong&gt;StartIoCancel&lt;/strong&gt;](wdm-startiocancel.md)"><strong>StartIoCancel</strong></a></p></td>
<td align="left"><p><a href="wdm-startiocancel.md" data-raw-source="[&lt;strong&gt;StartIoCancel&lt;/strong&gt;](wdm-startiocancel.md)"> <strong>StartIoCancel</strong> </a>规则指定驱动程序必须调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iosetstartioattributes" data-raw-source="[&lt;strong&gt;IoSetStartIoAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iosetstartioattributes)"> <strong>IoSetStartIoAttributes</strong> </a>与<em>无法</em>参数设置为<strong>FALSE</strong>之前，调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine" data-raw-source="[&lt;strong&gt;IoSetCancelRoutine&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine)"> <strong>IoSetCancelRoutine</strong> </a>与非<strong>NULL</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel" data-raw-source="[&lt;strong&gt;Cancel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)"><strong>取消</strong></a>例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-startiorecursion.md" data-raw-source="[&lt;strong&gt;StartIoRecursion&lt;/strong&gt;](wdm-startiorecursion.md)"><strong>StartIoRecursion</strong></a></p></td>
<td align="left"><p><a href="wdm-startiorecursion.md" data-raw-source="[&lt;strong&gt;StartIoRecursion&lt;/strong&gt;](wdm-startiorecursion.md)"> <strong>StartIoRecursion</strong> </a>规则指定的驱动程序，如果<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio" data-raw-source="[&lt;strong&gt;StartIo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)"> <strong>StartIo</strong> </a>例程包含对的调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket" data-raw-source="[&lt;strong&gt;IoStartNextPacket&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)"> <strong>IoStartNextPacket</strong></a>，该驱动程序必须先调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iosetstartioattributes" data-raw-source="[&lt;strong&gt;IoSetStartIoAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iosetstartioattributes)"> <strong>IoSetStartIoAttributes</strong> </a>与<em>DeferredStartIo</em>属性设置为<strong>，则返回 TRUE</strong>。 否则，可能会导致无限递归。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pnpremove.md" data-raw-source="[&lt;strong&gt;PnpRemove&lt;/strong&gt;](wdm-pnpremove.md)"><strong>PnpRemove</strong></a></p></td>
<td align="left"><p><a href="wdm-pnpremove.md" data-raw-source="[&lt;strong&gt;PnpRemove&lt;/strong&gt;](wdm-pnpremove.md)"> <strong>PnpRemove</strong> </a>规则指定驱动程序无法完成与 IRP_MN_SURPRISE_REMOVAL、 IRP_MN_CANCEL_REMOVE_DEVICE、 IRP_MN_CANCEL_STOP_DEVICE 或 IRP_MN_REMOVE_DEVICE 请求失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-pnpsurpriseremove.md" data-raw-source="[&lt;strong&gt;PnpSurpriseRemove&lt;/strong&gt;](wdm-pnpsurpriseremove.md)"><strong>PnpSurpriseRemove</strong></a></p></td>
<td align="left"><p><a href="wdm-pnpsurpriseremove.md" data-raw-source="[&lt;strong&gt;PnpSurpriseRemove&lt;/strong&gt;](wdm-pnpsurpriseremove.md)"> <strong>PnpSurpriseRemove</strong> </a>规则指定的驱动程序不会调用 IoDeleteDevice 或 IoDetachDevice 处理时<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal" data-raw-source="[&lt;strong&gt;IRP_MN_SURPRISE_REMOVAL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)"> <strong>IRP_MN_SURPRISE_REMOVAL</strong></a>请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-powerdownallocate.md" data-raw-source="[&lt;strong&gt;PowerDownAllocate&lt;/strong&gt;](wdm-powerdownallocate.md)"><strong>PowerDownAllocate</strong></a></p></td>
<td align="left"><p><a href="wdm-powerdownallocate.md" data-raw-source="[&lt;strong&gt;PowerDownAllocate&lt;/strong&gt;](wdm-powerdownallocate.md)"> <strong>PowerDownAllocate</strong> </a>规则指定 FDO 和 FIDO 的驱动程序不应分配内存时处理的 IRP_MN_SET_POWER 请求<strong>SystemPowerState</strong>转换从 s0 转到 [S1...S5]。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-powerdownfail.md" data-raw-source="[&lt;strong&gt;PowerDownFail&lt;/strong&gt;](wdm-powerdownfail.md)"><strong>PowerDownFail</strong></a></p></td>
<td align="left"><p><a href="wdm-powerdownfail.md" data-raw-source="[&lt;strong&gt;PowerDownFail&lt;/strong&gt;](wdm-powerdownfail.md)"> <strong>PowerDownFail</strong> </a>规则指定当设备关闭时，FDO 或 FIDO 驱动程序应不故障 IRP_MN_SET_POWER 请求。 此规则仅适用于 FDO 和 FIDO 驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-powerirpddis.md" data-raw-source="[&lt;strong&gt;PowerIrpDDIs&lt;/strong&gt;](wdm-powerirpddis.md)"><strong>PowerIrpDDIs</strong></a></p></td>
<td align="left"><p><a href="wdm-powerirpddis.md" data-raw-source="[&lt;strong&gt;PowerIrpDDIs&lt;/strong&gt;](wdm-powerirpddis.md)"> <strong>PowerIrpDDIs</strong> </a>规则指定的驱动程序处理时的系统或设备与 IRP_MN_SET_POWER IRP_MJ_POWER，它不应调用 DDIs 只能为在 passive_level 调用时调用的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-powerupfail.md" data-raw-source="[&lt;strong&gt;PowerUpFail&lt;/strong&gt;](wdm-powerupfail.md)"><strong>PowerUpFail</strong></a></p></td>
<td align="left"><p>PowerUpFail 规则指定当设备正在启动时，FDO 或 FIDO 驱动程序不应故障 IRP_MN_SET_POWER 请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-pnpirpcompletion.md" data-raw-source="[&lt;strong&gt;PnpIrpCompletion&lt;/strong&gt;](wdm-pnpirpcompletion.md)"><strong>PnpIrpCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-pnpirpcompletion.md" data-raw-source="[&lt;strong&gt;PnpIrpCompletion&lt;/strong&gt;](wdm-pnpirpcompletion.md)"> <strong>PnpIrpCompletion</strong> </a>规则验证 FDO 驱动程序将 PnP Irp 传递到较低的驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-wmicomplete.md" data-raw-source="[&lt;strong&gt;WmiComplete&lt;/strong&gt;](wdm-wmicomplete.md)"><strong>WmiComplete</strong></a></p></td>
<td align="left"><p><a href="wdm-wmicomplete.md" data-raw-source="[&lt;strong&gt;WmiComplete&lt;/strong&gt;](wdm-wmicomplete.md)"> <strong>WmiComplete</strong> </a>规则指定的处理时<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps" data-raw-source="[&lt;strong&gt;WMI minor IRP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)"> <strong>WMI 次要 IRP</strong></a>，驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)"> <strong>IoCompleteRequest</strong> </a>从返回之前<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;strong&gt;DispatchSystemControl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"> <strong>DispatchSystemControl</strong> </a>例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-wmiforward.md" data-raw-source="[&lt;strong&gt;WmiForward&lt;/strong&gt;](wdm-wmiforward.md)"><strong>WmiForward</strong></a></p></td>
<td align="left"><p><a href="wdm-wmiforward.md" data-raw-source="[&lt;strong&gt;WmiForward&lt;/strong&gt;](wdm-wmiforward.md)"> <strong>WmiForward</strong> </a>规则指定驱动程序必须转发<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps" data-raw-source="[&lt;strong&gt;WMI minor IRPs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)"> <strong>WMI 次要 Irp</strong> </a>的转发操作。</p></td>
</tr>
</tbody>
</table>

 

**若要选择 IrpProcessing 规则集**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...** .

2.  单击**规则**选项卡。下**规则集**，选择**IrpProcessing**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**IrpProcessing.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:IrpProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)并[Static Driver Verifier 命令 (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 





