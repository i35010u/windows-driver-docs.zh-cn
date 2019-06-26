---
title: LocalIrpProcessing 规则集 (WDM)
description: 使用这些规则来验证您的驱动程序正确地处理 I/O 请求数据包 (IRP) 创建的驱动程序。
ms.assetid: 2D10086F-4FCB-4BB1-AF63-49625DCA1A44
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9623c2c227d94cd23fe12567b77e7f80363fb329
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354807"
---
# <a name="localirpprocessing-rule-set-wdm"></a>LocalIrpProcessing 规则集 (WDM)


使用这些规则来验证您的驱动程序正确地处理 I/O 请求数据包 (IRP) 创建的驱动程序。

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
<td align="left"><p><a href="wdm-ioallocatecomplete.md" data-raw-source="[&lt;strong&gt;IoAllocateComplete&lt;/strong&gt;](wdm-ioallocatecomplete.md)"><strong>IoAllocateComplete</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocatecomplete.md" data-raw-source="[&lt;strong&gt;IoAllocateComplete&lt;/strong&gt;](wdm-ioallocatecomplete.md)"> <strong>IoAllocateComplete</strong> </a>规则指定一个驱动程序不应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)"> <strong>IoCompleteRequest</strong> </a>如果 IRP 创建了<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)"><strong>IoAllocateIrp</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-ioallocatefree.md" data-raw-source="[&lt;strong&gt;IoAllocateFree&lt;/strong&gt;](wdm-ioallocatefree.md)"><strong>IoAllocateFree</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocatefree.md" data-raw-source="[&lt;strong&gt;IoAllocateFree&lt;/strong&gt;](wdm-ioallocatefree.md)"> <strong>IoAllocateFree</strong> </a>规则指定一个驱动程序应使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)"> <strong>IoFreeIrp</strong> </a>只能对以前分配的 Irp<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)"> <strong>IoAllocateIrp</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-ioallocateforward.md" data-raw-source="[&lt;strong&gt;IoAllocateForward&lt;/strong&gt;](wdm-ioallocateforward.md)"><strong>IoAllocateForward</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateforward.md" data-raw-source="[&lt;strong&gt;IoAllocateForward&lt;/strong&gt;](wdm-ioallocateforward.md)"> <strong>IoAllocateForward</strong> </a>规则指定如果通过调用生成 IRP <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)"> <strong>IoAllocateIrp</strong></a>，驱动程序必须设置完成之前调用的例程<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"> <strong>IoCallDriver</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"> <strong>PoCallDriver</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion.md)"><strong>IoAllocateIrpSignalEventInCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion.md)"> <strong>IoAllocateIrpSignalEventInCompletion</strong> </a>规则指定驱动程序应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)"> <strong>KeSetEvent</strong> </a>中完成例程时<strong>Irp-&gt;PendingReturned</strong>设置标志，并开始处理本地创建异步 IRP 完成例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion2.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion2&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion2.md)"><strong>IoAllocateIrpSignalEventInCompletion2</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion2.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion2&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion2.md)"> <strong>IoAllocateIrpSignalEventInCompletion2</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)"> <strong>KeSetEvent</strong> </a>需要调用中完成例程当<strong>Irp-&gt;PendingReturned</strong>设置标志，并开始处理本地创建异步 IRP 完成例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion3.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion3&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion3.md)"><strong>IoAllocateIrpSignalEventInCompletion3</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion3.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion3&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion3.md)"> <strong>IoAllocateIrpSignalEventInCompletion3</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)"> <strong>KeSetEvent</strong> </a>需要调用中完成例程当<strong>Irp-&gt;PendingReturned</strong>设置标志，并开始处理本地创建异步 IRP 完成例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletiontimeout.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletionTimeout&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletiontimeout.md)"><strong>IoAllocateIrpSignalEventInCompletionTimeout</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletiontimeout.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletionTimeout&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletiontimeout.md)"> <strong>IoAllocateIrpSignalEventInCompletionTimeout</strong> </a>如果它检测到，此驱动程序将等到无限期地越低，规则将报告有缺陷，驱动程序返回，如 IRP 的事件必须是在完成例程中发出信号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuilddevicecontrolnofree.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlNoFree&lt;/strong&gt;](wdm-iobuilddevicecontrolnofree.md)"><strong>IoBuildDeviceControlNoFree</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuilddevicecontrolnofree.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlNoFree&lt;/strong&gt;](wdm-iobuilddevicecontrolnofree.md)"> <strong>IoBuildDeviceControlNoFree</strong> </a>规则指定的调用驱动程序<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)"> <strong>IoBuildDeviceIoControlRequest</strong> </a>不能调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)"> <strong>IoFreeIrp</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuilddevicecontrolwait.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlWait&lt;/strong&gt;](wdm-iobuilddevicecontrolwait.md)"><strong>IoBuildDeviceControlWait</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuilddevicecontrolwait.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlWait&lt;/strong&gt;](wdm-iobuilddevicecontrolwait.md)"> <strong>IoBuildDeviceControlWait</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)"> <strong>KeWaitForSingleObject</strong> </a>应调用例程，如果<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"> <strong>IoCallDriver</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"> <strong>PoCallDriver</strong> </a>返回 STATUS_PENDING。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuilddevicecontrolwaittimeout.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlWaitTimeout&lt;/strong&gt;](wdm-iobuilddevicecontrolwaittimeout.md)"><strong>IoBuildDeviceControlWaitTimeout</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuilddevicecontrolwaittimeout.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlWaitTimeout&lt;/strong&gt;](wdm-iobuilddevicecontrolwaittimeout.md)"> <strong>IoBuildDeviceControlWaitTimeout</strong> </a>如果它检测到，此驱动程序将等到无限期地越低，规则将报告有缺陷，驱动程序返回，如 IRP 的事件所需中发送信号完成例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuilddeviceiocontrolsetevent.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlSetEvent&lt;/strong&gt;](wdm-iobuilddeviceiocontrolsetevent.md)"><strong>IoBuildDeviceIoControlSetEvent</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuilddeviceiocontrolsetevent.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlSetEvent&lt;/strong&gt;](wdm-iobuilddeviceiocontrolsetevent.md)"> <strong>IoBuildDeviceIoControlSetEvent</strong> </a>规则指定的调用驱动程序<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)"> <strong>IoBuildDeviceIoControlRequest</strong> </a>不得调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)"> <strong>KeSetEvent</strong> </a>如果驱动程序提供指向调用方分配并初始化事件对象的指针。 <strong>KeSetEvent</strong>不需要为此 IRP 的调用由驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildfsdcomplete.md" data-raw-source="[&lt;strong&gt;IoBuildFsdComplete&lt;/strong&gt;](wdm-iobuildfsdcomplete.md)"><strong>IoBuildFsdComplete</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdcomplete.md" data-raw-source="[&lt;strong&gt;IoBuildFsdComplete&lt;/strong&gt;](wdm-iobuildfsdcomplete.md)"> <strong>IoBuildFsdComplete</strong> </a>规则指定一个驱动程序不应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)"> <strong>IoCompleteRequest</strong> </a>如果 IRP 创建了<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest" data-raw-source="[&lt;strong&gt;IoBuildAsynchronousFsdRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)"><strong>IoBuildAsynchronousFsdRequest</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildfsdforward.md" data-raw-source="[&lt;strong&gt;IoBuildFsdForward&lt;/strong&gt;](wdm-iobuildfsdforward.md)"><strong>IoBuildFsdForward</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdforward.md" data-raw-source="[&lt;strong&gt;IoBuildFsdForward&lt;/strong&gt;](wdm-iobuildfsdforward.md)"> <strong>IoBuildFsdForward</strong> </a>规则指定一个驱动程序调用之前，必须设置完成例程<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"> <strong>IoCallDriver</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"><strong>PoCallDriver</strong> </a>如果 IRP 生成通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest" data-raw-source="[&lt;strong&gt;IoBuildAsynchronousFsdRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)"> <strong>IoBuildAsynchronousFsdRequest</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildfsdfree.md" data-raw-source="[&lt;strong&gt;IoBuildFsdFree&lt;/strong&gt;](wdm-iobuildfsdfree.md)"><strong>IoBuildFsdFree</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdfree.md" data-raw-source="[&lt;strong&gt;IoBuildFsdFree&lt;/strong&gt;](wdm-iobuildfsdfree.md)"> <strong>IoBuildFsdFree</strong> </a>规则指定一个驱动程序应使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)"> <strong>IoFreeIrp</strong> </a>仅在它以前分配Irp上<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest" data-raw-source="[&lt;strong&gt;IoBuildAsynchronousFsdRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)"><strong>IoBuildAsynchronousFsdRequest</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion.md)"><strong>IoBuildFsdIrpSignalEventInCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion.md)"> <strong>IoBuildFsdIrpSignalEventInCompletion</strong> </a>规则指定驱动程序应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)"> <strong>KeSetEvent</strong> </a>中完成例程时<strong>Irp-&gt;PendingReturned</strong>设置标志，并开始处理本地创建异步 IRP 完成例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion2.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion2&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion2.md)"><strong>IoBuildFsdIrpSignalEventInCompletion2</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion2.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion2&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion2.md)"> <strong>IoBuildFsdIrpSignalEventInCompletion2</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)"> <strong>KeSetEvent</strong> </a>需要调用中完成例程当<strong>Irp-&gt;PendingReturned</strong>设置标志，并开始处理本地创建异步 IRP 完成例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion3.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion3&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion3.md)"><strong>IoBuildFsdIrpSignalEventInCompletion3</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion3.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion3&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion3.md)"> <strong>IoBuildFsdIrpSignalEventInCompletion3</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)"> <strong>KeSetEvent</strong> </a>需要调用中完成例程当<strong>Irp-&gt;PendingReturned</strong>设置标志，并开始处理本地创建异步 IRP 完成例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletiontimeout.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletionTimeout&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletiontimeout.md)"><strong>IoBuildFsdIrpSignalEventInCompletionTimeout</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletiontimeout.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletionTimeout&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletiontimeout.md)"> <strong>IoBuildFsdIrpSignalEventInCompletionTimeout</strong> </a>当驱动程序无限期地等到越低，规则将报告有缺陷，驱动程序返回，如 IRP 的事件所需中发送信号完成例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestnofree.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestNoFree&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestnofree.md)"><strong>IoBuildSynchronousFsdRequestNoFree</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestnofree.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestNoFree&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestnofree.md)"> <strong>IoBuildSynchronousFsdRequestNoFree</strong> </a>规则指定的调用驱动程序<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildsynchronousfsdrequest" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildsynchronousfsdrequest)"> <strong>IoBuildSynchronousFsdRequest</strong> </a>必须不调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)"> <strong>IoFreeIrp</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestwait.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestWait&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestwait.md)"><strong>IoBuildSynchronousFsdRequestWait</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestwait.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestWait&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestwait.md)"> <strong>IoBuildSynchronousFsdRequestWait</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)"> <strong>KeWaitForSingleObject</strong> </a>情况下应调用的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"> <strong>IoCallDriver</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"> <strong>PoCallDriver</strong> </a>返回 STATUS_PENDING。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestwaittimeout.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestWaitTimeout&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestwaittimeout.md)"><strong>IoBuildSynchronousFsdRequestWaitTimeout</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestwaittimeout.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestWaitTimeout&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestwaittimeout.md)"> <strong>IoBuildSynchronousFsdRequestWaitTimeout</strong> </a>如果它检测到，此驱动程序将等到无限期地越低，规则将报告有缺陷，驱动程序返回，如 IRP 的事件所需向发出信号，在完成例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-requestedpowerirp.md" data-raw-source="[&lt;strong&gt;RequestedPowerIrp&lt;/strong&gt;](wdm-requestedpowerirp.md)"><strong>RequestedPowerIrp</strong></a></p></td>
<td align="left"><p><a href="wdm-requestedpowerirp.md" data-raw-source="[&lt;strong&gt;RequestedPowerIrp&lt;/strong&gt;](wdm-requestedpowerirp.md)"> <strong>RequestedPowerIrp</strong> </a>规则指定该驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp" data-raw-source="[&lt;strong&gt;PoRequestPowerIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)"> <strong>PoRequestPowerIrp</strong> </a>与<code>*Irp</code>指针变量设置为<strong>NULL</strong>。</p></td>
</tr>
</tbody>
</table>

 

**若要选择 LocalIrpProcessing 规则集**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...** .

2.  单击**规则**选项卡。下**规则集**，选择**LocalIrpProcessing**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**LocalIrpProcessing.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:LocalIrpProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)并[Static Driver Verifier 命令 (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 





