---
title: LocalIrpProcessing 规则集 (WDM)
description: 使用这些规则验证驱动程序是否正确处理 (IRP) 的驱动程序创建的 i/o 请求包。
ms.assetid: 2D10086F-4FCB-4BB1-AF63-49625DCA1A44
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 50dba4e0177aea7248f0662888b3a6bda2f6d036
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382313"
---
# <a name="localirpprocessing-rule-set-wdm"></a>LocalIrpProcessing 规则集 (WDM)


使用这些规则验证驱动程序是否正确处理 (IRP) 的驱动程序创建的 i/o 请求包。

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
<td align="left"><p><a href="wdm-ioallocatecomplete.md" data-raw-source="[&lt;strong&gt;IoAllocateComplete&lt;/strong&gt;](wdm-ioallocatecomplete.md)"><strong>IoAllocateComplete</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocatecomplete.md" data-raw-source="[&lt;strong&gt;IoAllocateComplete&lt;/strong&gt;](wdm-ioallocatecomplete.md)"><strong>IoAllocateComplete</strong></a>规则指定如果 IRP 是使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)"><strong>IoAllocateIrp</strong></a>创建的，则驱动程序不应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-ioallocatefree.md" data-raw-source="[&lt;strong&gt;IoAllocateFree&lt;/strong&gt;](wdm-ioallocatefree.md)"><strong>IoAllocateFree</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocatefree.md" data-raw-source="[&lt;strong&gt;IoAllocateFree&lt;/strong&gt;](wdm-ioallocatefree.md)"><strong>IoAllocateFree</strong></a>规则指定，驱动程序只应在以前使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)"><strong>IoAllocateIrp</strong></a>分配的 irp 上使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)"><strong>IoFreeIrp</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-ioallocateforward.md" data-raw-source="[&lt;strong&gt;IoAllocateForward&lt;/strong&gt;](wdm-ioallocateforward.md)"><strong>IoAllocateForward</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateforward.md" data-raw-source="[&lt;strong&gt;IoAllocateForward&lt;/strong&gt;](wdm-ioallocateforward.md)"><strong>IoAllocateForward</strong></a>规则指定如果 IRP 是通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)"><strong>IoAllocateIrp</strong></a>生成的，则驱动程序必须在调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>PoCallDriver</strong></a>之前设置完成例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion.md)"><strong>IoAllocateIrpSignalEventInCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion.md)"><strong>IoAllocateIrpSignalEventInCompletion</strong></a>规则指定当设置了<strong>Irp- &gt; PendingReturned</strong>标志并且完成例程正在处理本地创建的异步 Irp 时，驱动程序应在完成例程中调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion2.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion2&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion2.md)"><strong>IoAllocateIrpSignalEventInCompletion2</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion2.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion2&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion2.md)"><strong>IoAllocateIrpSignalEventInCompletion2</strong></a>规则指定在设置了<strong>Irp- &gt; PendingReturned</strong>标志并且完成例程正在处理本地创建的异步 Irp 时，需要在完成例程中调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion3.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion3&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion3.md)"><strong>IoAllocateIrpSignalEventInCompletion3</strong></a></p></td>
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletion3.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletion3&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletion3.md)"><strong>IoAllocateIrpSignalEventInCompletion3</strong></a>规则指定在设置了<strong>Irp- &gt; PendingReturned</strong>标志并且完成例程正在处理本地创建的异步 Irp 时，需要在完成例程中调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-ioallocateirpsignaleventincompletiontimeout.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletionTimeout&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletiontimeout.md)"><strong>IoAllocateIrpSignalEventInCompletionTimeout</strong></a></p></td>
<td align="left"><p>如果 <a href="wdm-ioallocateirpsignaleventincompletiontimeout.md" data-raw-source="[&lt;strong&gt;IoAllocateIrpSignalEventInCompletionTimeout&lt;/strong&gt;](wdm-ioallocateirpsignaleventincompletiontimeout.md)"><strong>IoAllocateIrpSignalEventInCompletionTimeout</strong></a> 规则检测到此驱动程序将无限期等待，直到降低驱动程序返回，因为 IRP 的事件需要在完成例程中发出信号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuilddevicecontrolnofree.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlNoFree&lt;/strong&gt;](wdm-iobuilddevicecontrolnofree.md)"><strong>IoBuildDeviceControlNoFree</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuilddevicecontrolnofree.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlNoFree&lt;/strong&gt;](wdm-iobuilddevicecontrolnofree.md)"><strong>IoBuildDeviceControlNoFree</strong></a>规则指定调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)"><strong>IoBuildDeviceIoControlRequest</strong></a>的驱动程序不得调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)"><strong>IoFreeIrp</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuilddevicecontrolwait.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlWait&lt;/strong&gt;](wdm-iobuilddevicecontrolwait.md)"><strong>IoBuildDeviceControlWait</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuilddevicecontrolwait.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlWait&lt;/strong&gt;](wdm-iobuilddevicecontrolwait.md)"><strong>IoBuildDeviceControlWait</strong></a>规则指定如果<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>PoCallDriver</strong></a>返回 STATUS_PENDING，则应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)"><strong>KeWaitForSingleObject</strong></a>例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuilddevicecontrolwaittimeout.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlWaitTimeout&lt;/strong&gt;](wdm-iobuilddevicecontrolwaittimeout.md)"><strong>IoBuildDeviceControlWaitTimeout</strong></a></p></td>
<td align="left"><p>如果 <a href="wdm-iobuilddevicecontrolwaittimeout.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceControlWaitTimeout&lt;/strong&gt;](wdm-iobuilddevicecontrolwaittimeout.md)"><strong>IoBuildDeviceControlWaitTimeout</strong></a> 规则检测到此驱动程序将无限期等待，直到降低驱动程序返回，因为 IRP 的事件需要在完成例程中发出信号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuilddeviceiocontrolsetevent.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlSetEvent&lt;/strong&gt;](wdm-iobuilddeviceiocontrolsetevent.md)"><strong>IoBuildDeviceIoControlSetEvent</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuilddeviceiocontrolsetevent.md" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlSetEvent&lt;/strong&gt;](wdm-iobuilddeviceiocontrolsetevent.md)"><strong>IoBuildDeviceIoControlSetEvent</strong></a>规则指定如果驱动程序提供指向调用方分配和初始化的事件对象的指针，则调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)"><strong>IoBuildDeviceIoControlRequest</strong></a>的驱动程序不得调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a> 。 此 IRP 的驱动程序无需调用 <strong>KeSetEvent</strong> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildfsdcomplete.md" data-raw-source="[&lt;strong&gt;IoBuildFsdComplete&lt;/strong&gt;](wdm-iobuildfsdcomplete.md)"><strong>IoBuildFsdComplete</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdcomplete.md" data-raw-source="[&lt;strong&gt;IoBuildFsdComplete&lt;/strong&gt;](wdm-iobuildfsdcomplete.md)"><strong>IoBuildFsdComplete</strong></a>规则指定如果 IRP 是使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest" data-raw-source="[&lt;strong&gt;IoBuildAsynchronousFsdRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)"><strong>IoBuildAsynchronousFsdRequest</strong></a>创建的，则驱动程序不应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildfsdforward.md" data-raw-source="[&lt;strong&gt;IoBuildFsdForward&lt;/strong&gt;](wdm-iobuildfsdforward.md)"><strong>IoBuildFsdForward</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdforward.md" data-raw-source="[&lt;strong&gt;IoBuildFsdForward&lt;/strong&gt;](wdm-iobuildfsdforward.md)"><strong>IoBuildFsdForward</strong></a>规则指定如果 IRP 是通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest" data-raw-source="[&lt;strong&gt;IoBuildAsynchronousFsdRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)"><strong>IoBuildAsynchronousFsdRequest</strong></a>生成的，则必须在驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>PoCallDriver</strong></a>之前设置完成例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildfsdfree.md" data-raw-source="[&lt;strong&gt;IoBuildFsdFree&lt;/strong&gt;](wdm-iobuildfsdfree.md)"><strong>IoBuildFsdFree</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdfree.md" data-raw-source="[&lt;strong&gt;IoBuildFsdFree&lt;/strong&gt;](wdm-iobuildfsdfree.md)"><strong>IoBuildFsdFree</strong></a>规则指定，驱动程序应仅对先前使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest" data-raw-source="[&lt;strong&gt;IoBuildAsynchronousFsdRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)"><strong>IoBuildAsynchronousFsdRequest</strong></a>分配的 irp 使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)"><strong>IoFreeIrp</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion.md)"><strong>IoBuildFsdIrpSignalEventInCompletion</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion.md)"><strong>IoBuildFsdIrpSignalEventInCompletion</strong></a>规则指定当设置了<strong>Irp- &gt; PendingReturned</strong>标志并且完成例程正在处理本地创建的异步 Irp 时，驱动程序应在完成例程中调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion2.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion2&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion2.md)"><strong>IoBuildFsdIrpSignalEventInCompletion2</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion2.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion2&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion2.md)"><strong>IoBuildFsdIrpSignalEventInCompletion2</strong></a>规则指定在设置了<strong>Irp- &gt; PendingReturned</strong>标志并且完成例程正在处理本地创建的异步 Irp 时，需要在完成例程中调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion3.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion3&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion3.md)"><strong>IoBuildFsdIrpSignalEventInCompletion3</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletion3.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletion3&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletion3.md)"><strong>IoBuildFsdIrpSignalEventInCompletion3</strong></a>规则指定在设置了<strong>Irp- &gt; PendingReturned</strong>标志并且完成例程正在处理本地创建的异步 Irp 时，需要在完成例程中调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildfsdirpsignaleventincompletiontimeout.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletionTimeout&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletiontimeout.md)"><strong>IoBuildFsdIrpSignalEventInCompletionTimeout</strong></a></p></td>
<td align="left"><p>当驱动程序在较低的驱动程序返回之前， <a href="wdm-iobuildfsdirpsignaleventincompletiontimeout.md" data-raw-source="[&lt;strong&gt;IoBuildFsdIrpSignalEventInCompletionTimeout&lt;/strong&gt;](wdm-iobuildfsdirpsignaleventincompletiontimeout.md)"><strong>IoBuildFsdIrpSignalEventInCompletionTimeout</strong></a> 规则会报告缺陷，因为需要在完成例程中发出 IRP 的事件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestnofree.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestNoFree&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestnofree.md)"><strong>IoBuildSynchronousFsdRequestNoFree</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestnofree.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestNoFree&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestnofree.md)"><strong>IoBuildSynchronousFsdRequestNoFree</strong></a>规则指定调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)"><strong>IoBuildSynchronousFsdRequest</strong></a>的驱动程序不得调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp" data-raw-source="[&lt;strong&gt;IoFreeIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeirp)"><strong>IoFreeIrp</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestwait.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestWait&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestwait.md)"><strong>IoBuildSynchronousFsdRequestWait</strong></a></p></td>
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestwait.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestWait&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestwait.md)"><strong>IoBuildSynchronousFsdRequestWait</strong></a>规则指定在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)"><strong>PoCallDriver</strong></a>返回 STATUS_PENDING 的情况下应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject" data-raw-source="[&lt;strong&gt;KeWaitForSingleObject&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)"><strong>KeWaitForSingleObject</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-iobuildsynchronousfsdrequestwaittimeout.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestWaitTimeout&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestwaittimeout.md)"><strong>IoBuildSynchronousFsdRequestWaitTimeout</strong></a></p></td>
<td align="left"><p>如果 <a href="wdm-iobuildsynchronousfsdrequestwaittimeout.md" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequestWaitTimeout&lt;/strong&gt;](wdm-iobuildsynchronousfsdrequestwaittimeout.md)"><strong>IoBuildSynchronousFsdRequestWaitTimeout</strong></a> 规则检测到此驱动程序将无限期等待，直到降低驱动程序返回，因为 IRP 的事件需要在完成例程中发出信号。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-requestedpowerirp.md" data-raw-source="[&lt;strong&gt;RequestedPowerIrp&lt;/strong&gt;](wdm-requestedpowerirp.md)"><strong>RequestedPowerIrp</strong></a></p></td>
<td align="left"><p><a href="wdm-requestedpowerirp.md" data-raw-source="[&lt;strong&gt;RequestedPowerIrp&lt;/strong&gt;](wdm-requestedpowerirp.md)"><strong>RequestedPowerIrp</strong></a>规则指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp" data-raw-source="[&lt;strong&gt;PoRequestPowerIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)"><strong>PoRequestPowerIrp</strong></a> ，并将 <code>*Irp</code> 指针变量设置为<strong>NULL</strong>。</p></td>
</tr>
</tbody>
</table>

 

**选择 LocalIrpProcessing 规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 **LocalIrpProcessing**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**LocalIrpProcessing。 sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:LocalIrpProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

 

