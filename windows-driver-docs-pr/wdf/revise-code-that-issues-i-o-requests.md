---
title: 修改可发出 I/O 请求的代码
description: 修改可发出 I/O 请求的代码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5077ce23307c353a196a4bdf263077aa40ad6994
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839337"
---
# <a name="revise-code-that-issues-io-requests"></a>修改可发出 I/O 请求的代码


WDF 定义了一些方法，驱动程序可以使用这些方法来创建 i/o 请求并设置其格式。 下表总结了这些方法：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KMDF 方法</th>
<th align="left">操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforioctl" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForIoctl&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforioctl)"><strong>WdfIoTargetFormatRequestForIoctl</strong></a></p>
<p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctl" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctl&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctl)"><strong>WdfIoTargetFormatRequestForInternalIoctl</strong></a></p>
<p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctlothers" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctlOthers&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctlothers)"><strong>WdfIoTargetFormatRequestForInternalIoctlOthers</strong></a></p></td>
<td align="left">与手动设置下一个 i/o 堆栈位置的格式类似。</td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforread" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForRead&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforread)"><strong>WdfIoTargetFormatRequestForRead</strong></a></p>
<p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforwrite" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForWrite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforwrite)"><strong>WdfIoTargetFormatRequestForWrite</strong></a></p></td>
<td align="left">类似于 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest" data-raw-source="[&lt;strong&gt;IoBuildAsynchronousFsdRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)"><strong>IoBuildAsynchronousFsdRequest</strong></a>。</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendIoctlSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously)"><strong>WdfIoTargetSendIoctlSynchronously</strong></a></p>
<p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously)"><strong>WdfIoTargetSendInternalIoctlSynchronously</strong></a></p>
<p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlOthersSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously)"><strong>WdfIoTargetSendInternalIoctlOthersSynchronously</strong></a></p></td>
<td align="left">类似于 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)"><strong>IoBuildDeviceIoControlRequest</strong></a>，后跟 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>。</td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendReadSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)"><strong>WdfIoTargetSendReadSynchronously</strong></a></p>
<p><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendWriteSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously)"><strong>WdfIoTargetSendWriteSynchronously</strong></a></p></td>
<td align="left">类似于 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)"><strong>IoBuildSynchronousFsdRequest</strong></a>，后跟 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>。</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest" data-raw-source="[&lt;strong&gt;WdfRequestCancelSentRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest)"><strong>WdfRequestCancelSentRequest</strong></a></p></td>
<td align="left">类似于与<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>一起发送的 PIRP 的<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp" data-raw-source="[&lt;strong&gt;IoCancelIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)"><strong>IoCancelIrp</strong></a> 。 此框架提供锁，以确保 PIRP 在对 <strong>IoCallDriver</strong> 和 <strong>IoCancelIrp</strong>的调用之间不会完成或释放。</td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate" data-raw-source="[&lt;strong&gt;WdfRequestCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)"><strong>WdfRequestCreate</strong></a></td>
<td align="left">类似于 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)"><strong>IoAllocateIrp</strong></a>。 创建一个新的 WDFREQUEST 对象，设置特性，并返回调用方的句柄。</td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestformatrequestusingcurrenttype" data-raw-source="[&lt;strong&gt;WdfRequestFormatRequestUsingCurrentType&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestformatrequestusingcurrenttype)"><strong>WdfRequestFormatRequestUsingCurrentType</strong></a></td>
<td align="left">类似于 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioforwardirpsynchronously" data-raw-source="[&lt;strong&gt;IoForwardIrpSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioforwardirpsynchronously)"><strong>IoForwardIrpSynchronously</strong></a> ，但不调用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>;驱动程序必须调用 <a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)"><strong>WdfRequestSend</strong></a>。</td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)"><strong>WdfRequestSend</strong></a></td>
<td align="left">类似于 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioforwardirpsynchronously" data-raw-source="[&lt;strong&gt;IoForwardIrpSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioforwardirpsynchronously)"><strong>IoForwardIrpSynchronously</strong></a> ，但不调用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)"><strong>IoCallDriver</strong></a>;驱动程序必须调用 <a href="/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)"><strong>WdfRequestSend</strong></a>。</td>
</tr>
</tbody>
</table>

 

为了向另一个设备堆栈发送请求，WDF 驱动程序使用远程 i/o 目标。 有关如何初始化远程 i/o 目标的信息，请参阅 [初始化常规 I/o 目标](initializing-a-general-i-o-target.md)。

若要获取异步请求或通过调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)发送的任何请求的完成状态，驱动程序将调用 [**WdfRequestGetStatus**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetstatus)。 对于同步请求，它可以立即检索状态。 对于异步请求，驱动程序的 i/o 完成回调通常会检索状态。 有关同步发送请求或异步发送请求的详细信息，请参阅 [将 I/o 请求发送到一般 I/o 目标](sending-i-o-requests-to-general-i-o-targets.md)。

