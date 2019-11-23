---
title: 状态转换
description: 状态转换
ms.assetid: c71fd395-28aa-4421-9443-b5b0a1f3ac7e
keywords:
- 视频捕获 WDK AVStream，流状态
- 捕获视频 WDK AVStream，流状态
- 流状态 WDK 视频捕获
- 状态 WDK 视频捕获
- 状态转换 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b96de2b65d0760518b86a2cfba914bb7e7cdb82
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837696"
---
# <a name="state-transitions"></a>状态转换


若要确保资源分配有序，只允许使用部分可能的内核流状态转换。 下表列出了允许的转换以及 Stream 类微型驱动程序通常在此类转换过程中执行的任务。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>过渡</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>停止以暂停</p></td>
<td><p>分配资源。 完成转换到<strong>KSSTATE_PAUSE</strong>后，读取的 SRBs 将排队。</p></td>
</tr>
<tr class="even">
<td><p>暂停以运行</p></td>
<td><p>开始流式处理。</p></td>
</tr>
<tr class="odd">
<td><p>运行以暂停</p></td>
<td><p>停止流式处理。 未完成的读取 SRBs 保留在由微型驱动程序维护的队列中。</p></td>
</tr>
<tr class="even">
<td><p>暂停以停止</p></td>
<td><p>解除分配资源并完成所有未完成的读取 SRBs。 未使用图像填充的 SRBs 在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header" data-raw-source="[&lt;strong&gt;KSSTREAM_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)"><strong>KSSTREAM_HEADER</strong></a>结构的<strong>DataUsed</strong>成员中以零长度完成。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  ：在返回**KSSTATE\_停止**状态之前，转换可以在**KSSTATE\_PAUSE**和 KSSTATE 之间循环多次 **\_运行**状态。 视频捕获微型驱动程序应预期转换，例如：

 

KSSTATE\_STOP-&gt; **KSSTATE\_获取** -&gt; **KSSTATE\_暂停** -&gt; **KSSTATE\_运行** -&gt; **KSSTATE\_暂停** -&gt; **KSSTATE\_运行** -&gt; **KSSTATE\_暂停** -&gt; KSSTATE\_停止

当流处于**KSSTATE\_停止**状态时，微型驱动程序必须立即完成所有未完成的数据读取 SRBs。

由于用户模式应用程序在流式传输过程中可能会意外结束，因此所有 Stream 类微型驱动程序都必须接受并处理[**SRB\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-close-stream)来自 stream 类接口\_流请求。 在 Stream 类接口发送 SRB\_关闭\_流到微型驱动程序之前，它会通过微型驱动程序的**HwCancelPacket**例程取消所有未完成的缓冲区。 请注意，在应用程序终止之前，不能将流状态设置为**KSSTATE\_停止**。

请勿更新[**KS\_帧\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)， [**KS\_\_VBI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_vbi_frame_info)的**PICTURENUMBER**或**DropCount**成员\_信息，或[**KSPROPERTY\_DROPPEDFRAMES\_当前**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_droppedframes_current_s)从**KSSTATE**转换到 KSSTATE\_暂停到**KSSTATE\_运行**或**KSSTATE\_运行**到\_暂停。\_ 有关详细信息，请参阅[捕获视频](capturing-video.md)。

 

 




