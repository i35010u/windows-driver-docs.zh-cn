---
title: 处理流请求块
description: 处理流请求块
ms.assetid: fb4fda0d-54e9-4f1b-a78c-276e770189d5
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核 Srb
- 流式处理微型驱动程序 WDK Windows 2000 内核，Srb
- 微型驱动程序 WDK Windows 2000 内核流式处理 Srb
- Srb WDK 流式处理微型驱动程序
- 请参阅 SRB 或 Srb 流请求块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9f6e05efd619c3e10cdd1145d3456b5d5fb6e48
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384036"
---
# <a name="handling-stream-request-blocks"></a>处理流请求块





操作系统将调度到的类驱动程序在设备上的所有 I/O 请求。 在类驱动程序请求特定于硬件的信息从微型驱动程序通过将 Srb 传递给微型驱动程序。 在类驱动程序指定它在请求的操作**命令**流请求块的成员。

作为一个整体，微型驱动程序和内微型驱动程序，每个流都可能会收到输入/输出请求。 微型驱动程序必须提供[ *StrMiniReceiveDevicePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_receive_device_srb)例程来处理设备范围的请求。 每个流必须支持两个例程来处理 I/O 请求： 一个用于数据请求，另一个用于控制请求。 类驱动程序调用数据请求回调[ *StrMiniReceiveStreamDataPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_receive_device_srb)，以处理所有读取和写入请求流。 流的所有其他请求传递给[ **StrMiniReceiveStreamControlPacket**](https://docs.microsoft.com/previous-versions/ff568467(v=vs.85))。

如果类驱动程序正在处理的微型驱动程序同步，它流请求排队，并一次将其分派给微型驱动程序之一。 在类驱动程序维护三个单独的队列-一个用于设备请求，并分别用于流数据和控制请求。 微型驱动程序可能会发出信号，就可以从这些队列的一个新的请求，如下所示：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>请求类型</th>
<th>例程</th>
<th>NotificationType 参数的例程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>设备的请求</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassdevicenotification" data-raw-source="[&lt;strong&gt;StreamClassDeviceNotification&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassdevicenotification)"><strong>StreamClassDeviceNotification</strong></a></p></td>
<td><p>ReadyForNextDeviceRequest</p></td>
</tr>
<tr class="even">
<td><p>流控制请求</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassstreamnotification" data-raw-source="[&lt;strong&gt;StreamClassStreamNotification&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassstreamnotification)"><strong>StreamClassStreamNotification</strong></a></p></td>
<td><p>ReadyForNextStreamControlRequest</p></td>
</tr>
<tr class="odd">
<td><p>流数据请求</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassstreamnotification" data-raw-source="[&lt;strong&gt;StreamClassStreamNotification&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassstreamnotification)"><strong>StreamClassStreamNotification</strong></a></p></td>
<td><p>ReadyForNextStreamDataRequest</p></td>
</tr>
</tbody>
</table>

 

当在类驱动程序调用**StrMiniReceive*XXX*数据包**，关闭流请求块传递到微型驱动程序。 微型驱动程序的例程具有唯一的访问权的流请求块，直到它向发出信号，在类驱动程序已完成请求。

完成微型驱动程序处理的请求后，它应发出信号的类驱动程序已完成请求，如下所示：

1.  微型驱动程序应设置中请求的状态**状态**流请求块的字段。

2.  微型驱动程序应指示它已完成请求，通过调用[ **StreamClassDeviceNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassdevicenotification)或[ **StreamClassStreamNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassstreamnotification). 若要完成设备请求，微型驱动程序调用**StreamClassDeviceNotification**与*NotificationType* DeviceRequestComplete 参数。 若要完成的流请求，微型驱动程序调用**StreamClassStreamNotification**与*NotificationType* StreamRequestComplete 参数。

3.  如果在类驱动程序处理同步，并且微型驱动程序具有未尚未发出信号的类驱动程序已准备好在此队列上的另一个请求，它应立即实现。

微型驱动程序可以通过调用组合 2 和 3 [ **StreamClassCompleteRequestAndMarkQueueReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclasscompleterequestandmarkqueueready)。

微型驱动程序处理请求以异步方式，因此类驱动程序可能需要取消或超时请求。 出于这些目的，微型驱动程序必须提供[ *StrMiniCancelPacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_cancel_srb)和一个[ *StrMiniRequestTimeout* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_request_timeout_handler)例程。 它取消或超时请求时，类驱动程序将调用各自的微型驱动程序例程。

在类驱动程序由操作系统取消基础的 I/O 请求时取消的请求。 在类驱动程序超时请求花费很长时间来处理-它递减的秒数之前的计数器的超时时中的请求**TimeoutCounter**流请求块的成员。 如果微型驱动程序必须延迟很长的一段时间内处理的请求，则应设置**TimeoutCounter**为零-成员的类驱动程序然后将时间设置超时请求。 一旦微型驱动程序继续处理请求时，应重置**TimeoutCounter**等于**TimeoutOriginal**流请求块的成员。 微型驱动程序可以重置**TimeoutOriginal**若要更改的请求超时之前的时间长度。请参阅[ **HW\_流\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)有关详细信息。

 

 




