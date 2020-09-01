---
title: 处理流请求块
description: 处理流请求块
ms.assetid: fb4fda0d-54e9-4f1b-a78c-276e770189d5
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，SRBs
- 流式处理微型驱动程序 WDK Windows 2000 内核，SRBs
- 微型驱动程序 WDK Windows 2000 内核流式处理，SRBs
- SRBs WDK 流式处理微型驱动程序
- 流请求块，请参阅 SRB 或 SRBs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03861cd87ca7ffc9a5cb069ba897db84594fce74
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190567"
---
# <a name="handling-stream-request-blocks"></a>处理流请求块





操作系统将设备上所有 i/o 请求发送到类驱动程序。 类驱动程序通过将 SRBs 传递给微型驱动程序，进而从微型驱动程序请求特定于硬件的信息。 类驱动程序在流请求块的 **命令** 成员中指定它请求的操作。

微型驱动程序是一个整体，而微型驱动程序中的每个流都可以接收 i/o 请求。 微型驱动程序必须提供 [*StrMiniReceiveDevicePacket*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb) 例程来处理设备范围的请求。 每个流必须支持两个例程来处理 i/o 请求：一个用于数据请求，一个用于控制请求。 类驱动程序调用数据请求回调 [*StrMiniReceiveStreamDataPacket*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)来处理对流上的所有读取和写入请求。 流的所有其他请求会传递到 [**StrMiniReceiveStreamControlPacket**](/previous-versions/ff568467(v=vs.85))。

如果类驱动程序正在处理微型驱动程序的同步，它会将流请求排队，并一次将其调度到微型驱动程序。 类驱动程序维护三个单独的队列-一个用于设备请求，另一个用于流数据和控制请求。 微型驱动程序可能会发出信号，指示它已准备好从这些队列之一发出新请求，如下所示：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>请求类型</th>
<th>例程所返回的值</th>
<th>例程的 NotificationType 参数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>设备请求</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassdevicenotification" data-raw-source="[&lt;strong&gt;StreamClassDeviceNotification&lt;/strong&gt;](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassdevicenotification)"><strong>StreamClassDeviceNotification</strong></a></p></td>
<td><p>ReadyForNextDeviceRequest</p></td>
</tr>
<tr class="even">
<td><p>流控制请求</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification" data-raw-source="[&lt;strong&gt;StreamClassStreamNotification&lt;/strong&gt;](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification)"><strong>StreamClassStreamNotification</strong></a></p></td>
<td><p>ReadyForNextStreamControlRequest</p></td>
</tr>
<tr class="odd">
<td><p>流数据请求</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification" data-raw-source="[&lt;strong&gt;StreamClassStreamNotification&lt;/strong&gt;](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification)"><strong>StreamClassStreamNotification</strong></a></p></td>
<td><p>ReadyForNextStreamDataRequest</p></td>
</tr>
</tbody>
</table>

 

当类驱动程序调用 **StrMiniReceive*XXX*数据包**时，它会将流请求块移交给微型驱动程序。 微型驱动程序的例程具有对流请求块的唯一访问权限，直到它向类驱动程序发出请求。

当微型驱动程序处理完请求后，它应按照以下方式向类驱动程序发出请求：

1.  微型驱动程序应在流请求块的 " **状态** " 字段中设置请求的状态。

2.  微型驱动程序应通过调用 [**StreamClassDeviceNotification**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassdevicenotification) 或 [**StreamClassStreamNotification**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassstreamnotification)通知其已完成请求。 若要完成设备请求，微型驱动程序将使用*NotificationType*参数**StreamClassDeviceNotification**调用 DeviceRequestComplete。 若要完成流请求，微型驱动程序将使用 StreamRequestComplete 的*NotificationType*参数调用**StreamClassStreamNotification** 。

3.  如果类驱动程序正在处理同步，并且微型驱动程序尚未向类驱动程序发出通知，指示它已准备好用于该队列中的其他请求，现在应执行此操作。

微型驱动程序可以通过调用 [**StreamClassCompleteRequestAndMarkQueueReady**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclasscompleterequestandmarkqueueready)来组合2和3。

微型驱动程序异步处理请求，因此类驱动程序可能需要取消或超时请求。 出于这些目的，微型驱动程序必须提供 [*StrMiniCancelPacket*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_cancel_srb) 和 [*StrMiniRequestTimeout*](/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_request_timeout_handler) 例程。 类驱动程序在取消或超时请求时，将调用相应的微型驱动程序例程。

当操作系统取消基础 i/o 请求时，类驱动程序会取消请求。 类驱动程序发出的请求花费了太长时间来处理的请求数--它将在流请求块的 **TimeoutCounter** 成员中超时请求之前，将计数器递减多少秒。 如果微型驱动程序必须长时间延迟处理请求，则应将 **TimeoutCounter** 成员设置为零--类驱动程序将不会超时请求。 微型驱动程序继续处理请求后，它应将 **TimeoutCounter** 重置为等于流请求块的 **TimeoutOriginal** 成员。 微型驱动程序可以重置 **TimeoutOriginal** ，以更改请求超时前的时间长度。有关详细信息，请参阅 [**HW \_ STREAM \_ REQUEST \_ BLOCK**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block) 。

 

