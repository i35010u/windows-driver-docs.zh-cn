---
title: Storport 队列管理
description: Storport 队列管理
ms.assetid: 29fddcac-abc9-4aa4-8485-56120805ae34
keywords:
- Storport 驱动程序 WDK，队列管理
- 队列 WDK Storport
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1537e46f03af69dc8f9ea9d11ccd8696c44d1565
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188477"
---
# <a name="storport-queue-management"></a>Storport 队列管理


## <span id="ddk_storport_queue_management_kg"></span><span id="DDK_STORPORT_QUEUE_MANAGEMENT_KG"></span>


若要利用高性能存储适配器的功能，微型端口驱动程序必须控制其设备队列，以最大程度提高效率的方式暂停和恢复这些队列。

在 SCSI 端口队列模型中，队列管理是端口驱动程序的专用域。 在 Storport 队列模型中，端口驱动程序提供了多个队列管理支持例程，它们为微型端口驱动程序提供了大量队列管理控制。

在 Storport 队列模型中，所有请求都在每个逻辑单元队列的端口驱动程序中排队。 如果没有扩展的 SRB 支持，每个逻辑单元最多可以有255个未完成的请求。 否则，队列深度仅受可用系统资源或适配器功能的限制。 当达到为队列深度设置的限制时，Storport 将向该逻辑单元保留更多请求，直到该单元的未处理请求数降到队列最大值以下。

适配器可以具有的未处理请求数没有从 Storport 预定义的限制。 例如，如果某个适配器的队列深度为255，则连接到该适配器的55逻辑单元14025最多可以 (55 x 255) 请求。 有关端口驱动程序的队列模型的说明，请参阅下图。

![阐释端口驱动程序的队列模型的关系图](images/queues.png)

端口驱动程序的队列模型

如果适配器和逻辑单元已准备好接收请求，则系统会按该顺序调用微型端口驱动程序的 [**HwStorBuildIo**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio) 和 [**HwStorStartIo**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio) 例程。

与 SCSI 端口不同，Storport 允许微型端口驱动程序向端口驱动程序通知繁忙情况。 这些通信由以下八个例程处理，使微型端口驱动程序可以在逻辑单元或适配器处于暂停或繁忙状态时发出信号。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Storport 例程</th>
<th align="left">执行的操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportpausedevice" data-raw-source="[&lt;strong&gt;StorPortPauseDevice&lt;/strong&gt;](/windows-hardware/drivers/ddi/storport/nf-storport-storportpausedevice)"><strong>StorPortPauseDevice</strong></a></p></td>
<td align="left"><p>将设备暂停指定的一段时间。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportresumedevice" data-raw-source="[&lt;strong&gt;StorPortResumeDevice&lt;/strong&gt;](/windows-hardware/drivers/ddi/storport/nf-storport-storportresumedevice)"><strong>StorPortResumeDevice</strong></a></p></td>
<td align="left"><p>恢复暂停的设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportpause" data-raw-source="[&lt;strong&gt;StorPortPause&lt;/strong&gt;](/windows-hardware/drivers/ddi/storport/nf-storport-storportpause)"><strong>StorPortPause</strong></a></p></td>
<td align="left"><p>在指定的时间段内暂停适配器。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportresume" data-raw-source="[&lt;strong&gt;StorPortResume&lt;/strong&gt;](/windows-hardware/drivers/ddi/storport/nf-storport-storportresume)"><strong>StorPortResume</strong></a></p></td>
<td align="left"><p>恢复暂停的适配器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportdevicebusy" data-raw-source="[&lt;strong&gt;StorPortDeviceBusy&lt;/strong&gt;](/windows-hardware/drivers/ddi/storport/nf-storport-storportdevicebusy)"><strong>StorPortDeviceBusy</strong></a></p></td>
<td align="left"><p>使设备处于繁忙状态，直到设备队列已完成指定数目的 i/o 请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportdeviceready" data-raw-source="[&lt;strong&gt;StorPortDeviceReady&lt;/strong&gt;](/windows-hardware/drivers/ddi/storport/nf-storport-storportdeviceready)"><strong>StorPortDeviceReady</strong></a></p></td>
<td align="left"><p>让繁忙设备准备好接收请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportbusy" data-raw-source="[&lt;strong&gt;StorPortBusy&lt;/strong&gt;](/windows-hardware/drivers/ddi/storport/nf-storport-storportbusy)"><strong>StorPortBusy</strong></a></p></td>
<td align="left"><p>使适配器处于繁忙状态，直到它完成了指定数目的 i/o 请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportready" data-raw-source="[&lt;strong&gt;StorPortReady&lt;/strong&gt;](/windows-hardware/drivers/ddi/storport/nf-storport-storportready)"><strong>StorPortReady</strong></a></p></td>
<td align="left"><p>让繁忙的适配器准备好接收请求。</p></td>
</tr>
</tbody>
</table>

 

设备暂停或繁忙时，端口驱动程序不会向设备发送请求。 如果微型端口驱动程序完成了处于繁忙状态的请求 (SRB \_ 状态 \_ 繁忙或 SCSISTAT \_ 繁忙) ，则端口驱动程序会无限次重试请求，直到请求失败或完成。

除了提供一组在 SCSI 端口队列模型中不可用的显式队列管理例程以外，Storport 队列模型不使用 SCSI 端口所采用的隐式队列管理例程。 具体而言，将忽略 **NextRequest** 和 **NextLuRequest** 通知。

 

