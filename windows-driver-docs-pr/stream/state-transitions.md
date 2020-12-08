---
title: 状态转换
description: 状态转换
keywords:
- 视频捕获 WDK AVStream，流状态
- 捕获视频 WDK AVStream，流状态
- 流状态 WDK 视频捕获
- 状态 WDK 视频捕获
- 状态转换 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de5efa2096c9345832aba79bd1c129c7f5bd09db
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820439"
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
<th>切换</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>停止以暂停</p></td>
<td><p>分配资源。 完成转换到 <strong>KSSTATE_PAUSE</strong> 后，读取的 SRBs 将排队。</p></td>
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
<td><p>解除分配资源并完成所有未完成的读取 SRBs。 未使用图像填充的 SRBs 在<a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header" data-raw-source="[&lt;strong&gt;KSSTREAM_HEADER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)"><strong>KSSTREAM_HEADER</strong></a>结构的<strong>DataUsed</strong>成员中以零长度完成。</p></td>
</tr>
</tbody>
</table>

 

**注意**：在返回 **KSSTATE \_ 停止** 状态之前，转换可能会在 **KSSTATE \_ PAUSE** 和 **KSSTATE \_ 运行** 状态之间循环多次。 视频捕获微型驱动程序应预期转换，例如：

 

KSSTATE \_ &gt; **KSSTATE \_ 获取**  - &gt; **KSSTATE \_ 暂停**  - &gt; **KSSTATE \_ 运行**  - &gt; **KSSTATE \_ 暂停**  - &gt; **KSSTATE \_ 运行**  - &gt; **KSSTATE \_ 暂停**  - &gt; KSSTATE \_ 停止

当流处于 **KSSTATE \_ 停止** 状态时，微型驱动程序必须立即完成所有未完成的数据读取 SRBs。

由于用户模式应用程序在流式传输过程中可能会意外结束，因此所有 Stream 类微型驱动程序都必须随时接受并处理来自 Stream 类接口的 [**SRB \_ 关闭 \_ 流**](./srb-close-stream.md) 请求。 在 Stream 类接口将 SRB \_ CLOSE \_ 流发送到微型驱动程序之前，它会通过微型驱动程序的 **HwCancelPacket** 例程取消所有未完成的缓冲区。 请注意，在应用程序终止之前，不能将流状态设置为 **KSSTATE \_ STOP** 。

请勿更新 [**ks \_ 帧 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)的 **PictureNumber** 或 **DropCount** 成员， [**ks \_ VBI \_ 帧 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_vbi_frame_info)或 [**KSPROPERTY \_ DROPPEDFRAMES \_ 当前 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_droppedframes_current_s)的从 **KSSTATE \_ 暂停** 转换到 **KSSTATE \_ 运行**，或 **KSSTATE \_ 运行** 到 KSSTATE \_ 暂停。 有关详细信息，请参阅 [捕获视频](capturing-video.md)。

