---
title: Storport 队列管理
description: Storport 队列管理
ms.assetid: 29fddcac-abc9-4aa4-8485-56120805ae34
keywords:
- Storport 驱动程序 WDK，队列管理
- 队列 WDK Storport
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f84c0dd1a69eab9e97f7150c9030eb0708d6c8b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386117"
---
# <a name="storport-queue-management"></a>Storport 队列管理


## <span id="ddk_storport_queue_management_kg"></span><span id="DDK_STORPORT_QUEUE_MANAGEMENT_KG"></span>


若要利用的功能的高性能存储适配器，微型端口驱动程序必须对进行控制其设备队列，暂停和恢复这些队列将最大限度地提高效率的方式。

在 SCSI 端口队列模型中，队列管理是端口驱动程序的排他域。 在 Storport 队列模型中，端口驱动程序提供了多个队列管理支持例程提供大量的队列的管理控制的微型端口驱动程序。

在 Storport 队列模型中，在逻辑单元队列中的端口驱动程序中排队的所有请求。 如果没有扩展 SRB 支持，每个逻辑单元可以具有最多为 255 未完成的请求。 否则，仅受可用系统资源或该适配器的功能限制的队列深度。 达到限制为的队列深度设置后，Storport 之前未完成请求到的单元数下降到低于最大队列保存的后续请求，到该逻辑单元。

没有预定义的限制从 Storport 上一个适配器可以具有的未完成请求数。 例如，使用附加到该队列深度为 255 的 55 个逻辑单位的适配器可以将发布到 14,025 (55 x 255) 的最大请求一次。 请参阅下图以了解端口驱动程序的队列模型的说明。

![说明端口驱动程序的队列模型关系图](images/queues.png)

端口驱动程序的队列模型

如果适配器和逻辑单元都准备好接收请求，系统会调用微型端口驱动程序[ **HwStorBuildIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_buildio)并[ **HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)例程按该顺序。

SCSI 端口与 Storport 允许微型端口驱动程序以通知端口驱动程序的繁忙的条件。 这些通信都由以下八个例程，允许的逻辑单元或适配器是已暂停或繁忙时发出信号通知的微型端口驱动程序处理。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Storport 例程</th>
<th align="left">执行操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportpausedevice" data-raw-source="[&lt;strong&gt;StorPortPauseDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportpausedevice)"><strong>StorPortPauseDevice</strong></a></p></td>
<td align="left"><p>为指定的时间段，设备暂停。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportresumedevice" data-raw-source="[&lt;strong&gt;StorPortResumeDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportresumedevice)"><strong>StorPortResumeDevice</strong></a></p></td>
<td align="left"><p>恢复已暂停的设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportpause" data-raw-source="[&lt;strong&gt;StorPortPause&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportpause)"><strong>StorPortPause</strong></a></p></td>
<td align="left"><p>暂停指定的时间段的适配器。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportresume" data-raw-source="[&lt;strong&gt;StorPortResume&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportresume)"><strong>StorPortResume</strong></a></p></td>
<td align="left"><p>恢复暂停的适配器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportdevicebusy" data-raw-source="[&lt;strong&gt;StorPortDeviceBusy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportdevicebusy)"><strong>StorPortDeviceBusy</strong></a></p></td>
<td align="left"><p>使设备繁忙，直到设备队列已完成指定的数量的 I/O 请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportdeviceready" data-raw-source="[&lt;strong&gt;StorPortDeviceReady&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportdeviceready)"><strong>StorPortDeviceReady</strong></a></p></td>
<td align="left"><p>准备好再次接收请求将忙碌的设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportbusy" data-raw-source="[&lt;strong&gt;StorPortBusy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportbusy)"><strong>StorPortBusy</strong></a></p></td>
<td align="left"><p>使适配器繁忙，直到它完成指定的数量的 I/O 请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportready" data-raw-source="[&lt;strong&gt;StorPortReady&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportready)"><strong>StorPortReady</strong></a></p></td>
<td align="left"><p>准备好再次接收请求将繁忙的适配器。</p></td>
</tr>
</tbody>
</table>

 

已暂停或忙设备时，端口驱动程序将没有请求发送到设备。 如果微型端口驱动程序完成时忙状态的请求 (SRB\_状态\_忙碌或 SCSISTAT\_繁忙)，则端口驱动程序将重试请求数量不确定的次数，直到该请求会失败或完成。

除了提供的一组在 SCSI 端口队列模型中不可用的显式队列管理例程，Storport 队列模型不使用 SCSI 端口所采用的隐式的队列管理例程。 具体而言， **NextRequest**并**NextLuRequest**通知将被忽略。

 

 




