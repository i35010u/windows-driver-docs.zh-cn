---
title: 使用视频捕获设备使用的筛选器
description: 使用视频捕获设备使用的筛选器
ms.assetid: 797f855d-5c6f-45bc-8b4a-f03543fa196d
keywords:
- 筛选图形配置 WDK 视频捕获，DirectShow
- DirectShow WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4224abfd47a8a248c4633c6e8ddeadd2d98bb11f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523498"
---
# <a name="filters-used-with-the-video-capture-devices"></a>使用视频捕获设备使用的筛选器


Microsoft DirectShow 是视频捕获微型驱动程序的常见客户端。 用户模式下 DirectShow 筛选器公开视频捕获微型驱动程序对用户模式应用程序中包含的功能。

Microsoft 提供了使用 Stream 类微型驱动程序，以公开的基本功能的视频捕获微型驱动程序的四个 DirectShow 筛选器：

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>筛选器功能</th>
<th>支持的内核流式处理的属性集</th>
<th>用途</th>
<th>DLL</th>
<th>公开 DirectShow 接口</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>视频视频</p></td>
<td><p>PROPSETID_VIDCAP_DROPPEDFRAMES</p>
<p>PROPSETID_VIDCAP_VIDEOCOMPRESSION</p>
<p>PROPSETID_VIDCAP_VIDEOCONTROL</p>
<p>PROPSETID_VIDCAP_VIDEODECODER</p>
<p>PROPSETID_VIDCAP_CAMERAMCONTROL</p>
<p>PROPSETID_VIDCAP_VIDEOPROCAMP</p></td>
<td><p>提供的数字视频数据的输出流和辅助数据流。</p></td>
<td><p><em>KsProxy.ax</em></p></td>
<td><p><strong>IAMAnalogVideoDecoder</strong></p>
<p><strong>IAMCameraControl</strong></p>
<p><strong>IAMVideoProcAmp</strong></p>
<p><strong>IAMDroppedFrames</strong></p>
<p><strong>IAMStreamConfig</strong></p>
<p><strong>IAMVideoControl</strong></p>
<p><strong>IAMVideoCompression</strong></p>
<p><strong>IAMBufferNegotiation</strong></p></td>
</tr>
<tr class="even">
<td><p>电视优化</p></td>
<td><p>PROPSETID_TUNER</p></td>
<td><p>提供的模拟电视、 数字电视、 FM 的优化控制，并将调谐器。</p></td>
<td><p><em>KsTvTune.ax</em></p></td>
<td><p><strong>IAMTVTuner</strong></p></td>
</tr>
<tr class="odd">
<td><p>电视音频</p></td>
<td><p>PROPSETID_VIDCAP_TVAUDIO</p></td>
<td><p>提供了控制电视音频等 SAP 所选内容。</p></td>
<td><p><em>KsXBar.ax</em></p></td>
<td><p><strong>IAMTVAudio</strong></p></td>
</tr>
<tr class="even">
<td><p>横线</p></td>
<td><p>PROPSETID_VIDCAP_CROSSBAR</p></td>
<td><p>提供视频和音频流的路由。</p></td>
<td><p><em>KsXBar.ax</em></p></td>
<td><p><strong>IAMCrossbar</strong></p></td>
</tr>
</tbody>
</table>

 

这些筛选器，以及它们公开 （视频捕获、 电视/单选优化、 电视音频和纵横制） 的功能的每个筛选器关系图中显示为单独的筛选器公开独特的接口。

有关上述表中列出的 DirectShow 接口的详细信息，请参阅 DirectShow 软件开发工具包 (SDK)。 DirectShow SDK 文档还包括演示如何构造 WDM 和 VfW 捕获关系图的完整范围的示例应用程序 (AMCAP)。

 

 




