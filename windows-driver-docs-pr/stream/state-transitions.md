---
title: 状态转换
description: 状态转换
ms.assetid: c71fd395-28aa-4421-9443-b5b0a1f3ac7e
keywords:
- WDK AVStream 的视频捕获，流状态
- 捕获视频 WDK AVStream，流式传输状态
- 流状态 WDK 视频捕获
- 指出 WDK 视频捕获
- WDK 视频捕获的状态转换
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1319c5faecf838ded6ade6b0208b4d6cbd26fa0b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333968"
---
# <a name="state-transitions"></a>状态转换


若要确保有序的资源分配，请允许可能内核流式处理状态转换的一个子集。 下表列出了允许的转换以及 Stream 类微型驱动程序通常在此类转换过程中执行的任务。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>转换</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>停止暂停</p></td>
<td><p>分配的资源。 Srb 排队到转换后的读<strong>KSSTATE_PAUSE</strong>已完成。</p></td>
</tr>
<tr class="even">
<td><p>暂停运行</p></td>
<td><p>开始流式处理。</p></td>
</tr>
<tr class="odd">
<td><p>若要暂停的运行</p></td>
<td><p>停止流式处理。 未完成读取 Srb 保留在队列中维护的微型驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>若要停止的暂停</p></td>
<td><p>解除分配资源并完成所有未完成读取 Srb。 Srb 尚未填充的映像已完成，但在长度为零<strong>DataUsed</strong>的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff567138" data-raw-source="[&lt;strong&gt;KSSTREAM_HEADER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567138)"> <strong>KSSTREAM_HEADER</strong> </a>结构。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  :转换可以将多个时间周期之间**KSSTATE\_暂停**并**KSSTATE\_运行**状态才会回到**KSSTATE\_停止**状态。 例如，视频捕获微型驱动程序应该会转换：

 

KSSTATE\_停止-&gt; **KSSTATE\_ACQUIRE**  - &gt; **KSSTATE\_暂停** - &gt; **KSSTATE\_运行** - &gt; **KSSTATE\_暂停** - &gt; **KSSTATE\_运行** - &gt; **KSSTATE\_暂停** - &gt; KSSTATE\_停止

当流处于**KSSTATE\_停止**状态中时，微型驱动程序必须立即完成所有未完成的数据读取 Srb。

在用户模式应用程序可以流式处理时意外结束，因为所有 Stream 类微型驱动程序必须接受并处理[ **SRB\_关闭\_流**](https://msdn.microsoft.com/library/windows/hardware/ff568165)从请求在任何时间 Stream 类接口。 之前 Stream 类接口发送 SRB\_关闭\_流到微型驱动程序，它会取消通过微型驱动程序的所有未完成的缓冲区**HwCancelPacket**例程。 请注意，无法将流状态设置为**KSSTATE\_停止**在应用程序终止之前。

不会更新**PictureNumber**或**DropCount**的成员[ **KS\_帧\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567645)， [ **KS\_VBI\_帧\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567694)，或[ **KSPROPERTY\_DROPPEDFRAMES\_当前\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565138)上从过渡**KSSTATE\_暂停**到**KSSTATE\_运行**或**KSSTATE\_运行**KSSTATE 到\_暂停。 有关详细信息，请参阅[捕获视频](capturing-video.md)。

 

 




