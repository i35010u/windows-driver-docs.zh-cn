---
title: 与视频捕获设备配合使用的筛选器
description: 与视频捕获设备配合使用的筛选器
keywords:
- 筛选器关系图配置 WDK 视频捕获，DirectShow
- DirectShow WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11cb4d7baeed875aaea7a262fb9cb1a78bd7f149
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823703"
---
# <a name="filters-used-with-the-video-capture-devices"></a>与视频捕获设备配合使用的筛选器


Microsoft DirectShow 是视频捕获微型驱动程序的常见客户端。 用户模式 DirectShow 筛选器将视频捕获微型驱动程序中包含的功能公开给用户模式应用程序。

Microsoft 提供了四个 DirectShow 筛选器，它们使用 Stream 类微型驱动程序来公开底层视频捕获微型驱动程序功能：

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
<th>筛选功能</th>
<th>内核流支持的属性集</th>
<th>目的</th>
<th>DLL</th>
<th>已公开 DirectShow 接口</th>
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
<td><p>提供数字视频数据和辅助数据流的输出流。</p></td>
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
<td><p>电视调谐</p></td>
<td><p>PROPSETID_TUNER</p></td>
<td><p>提供模拟电视、数字电视、FM 和 AM 调谐器的优化控制。</p></td>
<td><p><em>KsTvTune.ax</em></p></td>
<td><p><strong>IAMTVTuner</strong></p></td>
</tr>
<tr class="odd">
<td><p>TV 音频</p></td>
<td><p>PROPSETID_VIDCAP_TVAUDIO</p></td>
<td><p>提供电视音频（如 SAP 选择）的控制。</p></td>
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

 

其中每个筛选器及其公开的功能 (视频捕获、电视/无线电调谐、电视音频和纵横比) 在筛选器关系图中显示为一个单独的筛选器，该筛选器公开了唯一接口。

有关上表中列出的 DirectShow 接口的详细信息，请参阅 DirectShow 软件开发工具包 (SDK) 。 DirectShow SDK 文档还包括一个 (AMCAP) 的示例应用程序，该示例演示如何构造 WDM 和 VfW 捕获关系图的整个范围。

 

 




