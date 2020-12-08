---
title: 输入流
description: 输入流
keywords:
- 输入流 WDK DVD 解码器
- DVD 包 WDK DVD 解码器
- 子画面流 WDK DVD 解码器
- SDD 音频输入流 WDK DVD 解码器
- DTS 音频输入流 WDK DVD 解码器
- LPCM 音频输入流 WDK DVD 解码器
- AC 3 WDK DVD 解码器
- MPEG2 视频输入流 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0831d8e0651abc0976f9f5b53d27c2cf386be4a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790265"
---
# <a name="input-streams"></a>输入流





DVD 输入流作为加密 DVD 包的数组提供给微型驱动程序。 包是在 DVD 规范中定义的。 请注意，PACK 的系统时钟引用 (SCR) 字段设置为零，因为 Microsoft 的 DVD 体系结构使用 "主时钟" 模式进行音频和视频同步。 通常，DVD 解码器微型驱动程序的音频流提供主时钟。 有关详细信息，请参阅 [主时钟](master-clock.md)。

DVD 数据流通过 [**SRB \_ 写入 \_ 数据**](./srb-write-data.md) 请求发送到微型驱动程序。 有关 SRB 请求的详细信息，请参阅 [处理流请求块](handling-stream-request-blocks.md) 和 [Stream 类 SRB 引用](./stream-class-srb-reference.md)。 硬件应支持散播/聚集 DMA，因为多个 DVD 包可能存在于单个请求数据包中。

下表描述了 DVD 电影使用的 MPEG2 视频输入流媒体类型：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主要格式 GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>次要格式 GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_MPEG2_VIDEO</p></td>
</tr>
<tr class="odd">
<td><p>格式块说明符 GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_MPEG2_VIDEO</p></td>
</tr>
<tr class="even">
<td><p>格式块结构</p></td>
<td><p>MPEG2VIDEOINFO</p>
<div>
 
</div>
VIDEOINFO2 结构的 (超集。 还指示 MPEG 配置文件和级别。 ) </td>
</tr>
</tbody>
</table>

 

下表描述了 DVD 电影使用的 AC 3 音频输入流媒体类型：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主要格式 GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>次要格式 GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_AC3_AUDIO</p></td>
</tr>
<tr class="odd">
<td><p>格式块说明符 GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p>
<p> (请注意，此行为应发生变化。 ) </p></td>
</tr>
<tr class="even">
<td><p>格式块结构</p></td>
<td><p>KSDATAFORMAT_WAVEFORMATEX</p>
<div>
 
</div>
WaveFormatEx 的超集
<p> (两个以上的通道。 下组合描述符。 ) </p></td>
</tr>
</tbody>
</table>

 

下表描述了 DVD 电影使用的 LPCM 音频输入流媒体类型：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主要格式 GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>次要格式 GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_LPCM_AUDIO</p></td>
</tr>
<tr class="odd">
<td><p>格式块说明符 GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p></td>
</tr>
<tr class="even">
<td><p>格式块结构</p></td>
<td><p>KSDATAFORMAT_WAVEFORMATEX</p></td>
</tr>
</tbody>
</table>

 

下表描述了 DVD 电影使用的 DTS 音频输入流媒体类型：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主要格式 GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>次要格式 GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_DTS_AUDIO</p></td>
</tr>
<tr class="odd">
<td><p>格式块说明符 GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p>
<p> (请注意，此行为应发生变化。 ) </p></td>
</tr>
<tr class="even">
<td><p>格式块结构</p></td>
<td><p>KSDATAFORMAT_WAVEFORMATEX</p>
<div>
 
</div>
WaveFormatEx 的超集
<p> (两个以上的通道。 下组合描述符。 ) </p></td>
</tr>
</tbody>
</table>

 

下表描述了 DVD 电影使用的 SDD 音频输入流媒体类型：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主要格式 GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>次要格式 GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_SDDS_AUDIO</p></td>
</tr>
<tr class="odd">
<td><p>格式块说明符 GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p>
<p> (请注意，此行为应发生变化。 ) </p></td>
</tr>
<tr class="even">
<td><p>格式块结构</p></td>
<td><p>KSDATAFORMAT_WAVEFORMATEX</p>
<div>
 
</div>
WaveFormatEx 的超集
<p> (两个以上的通道。 下组合描述符。 ) </p></td>
</tr>
</tbody>
</table>

 

下表描述了 DVD 电影使用的子画面流媒体类型：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主要格式 GUID</p></td>
<td><p>KSDATAFORMAT_TYPE_DVD_ENCRYPTED_PACK</p></td>
</tr>
<tr class="even">
<td><p>次要格式 GUID</p></td>
<td><p>KSDATAFORMAT_SUBTYPE_SUBPICTURE</p></td>
</tr>
<tr class="odd">
<td><p>格式块说明符 GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NONE</p></td>
</tr>
<tr class="even">
<td><p>格式块结构</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

 

对于子画面突出显示，调色板信息和突出显示信息作为属性传递。 子画面数据流由 DVD 规范提供的数据数据包组成。 虽然 PACK 标头被去除，但仍会提供。

Microsoft 提供的 DVD 导航器筛选器分析所有按钮和键盘信息，并且在任何给定时间只将一个突出显示的矩形向下传递到子画面解码器。 因此，将突出显示信息发送到解码器的频率比 DVD 流中显示的信息更多。 这不同于 DVD 规范。

DVD 导航器/拆分器筛选器处理所有击键信息，并在每次按钮状态发生更改时发送新的突出显示信息。 信息一次仅描述一个按钮的一种模式。 它包括屏幕像素坐标中的显示矩形或子画面（如果存在）的显示。 [**KSPROPERTY \_ SPHLI**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksproperty_sphli)结构还包含颜色和对比度信息，但仅适用于当前所选按钮的当前状态。 格式是在 DVD 规范中定义的。

突出显示信息以异步方式到达数据流。 DVD 解码器微型驱动程序必须使用突出显示开始和结束时间戳将突出显示信息关联到相关的子画面信息（如果有）。 如果 DVD 解码器微型驱动程序尚未收到请求的时间戳的任何子画面流信息，则解码器会假设突出显示信息是独立的，不适用于子画面。 在这种情况下，可以假设颜色和对比度信息的颜色完全相同。

突出显示的信息包含开始和结束时间戳。 它们的单位与其他时间戳的单位相同，但有两个例外：0xFFFFFFFF 的开始时间戳表示突出显示属性在接收时有效，而在收到下一个突出显示之前，0xFFFFFFFF 的结束时间戳表示高光属性有效。

 

