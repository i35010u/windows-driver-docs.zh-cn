---
title: 输入的流
description: 输入的流
ms.assetid: 0aa378d8-e7e2-4555-b541-dd1ed77b4a12
keywords:
- 输入的流的 WDK DVD 解码器
- DVD 包 WDK DVD 解码器
- 子流 WDK DVD 解码器图
- SDD 音频输入流的 WDK DVD 解码器
- DTS 音频输入流的 WDK DVD 解码器
- LPCM 音频输入流的 WDK DVD 解码器
- Ac-3 WDK DVD 解码器
- MPEG2 视频输入流的 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0740694167f9aea25a7bc31b7f08d8c9ae7024a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546256"
---
# <a name="input-streams"></a>输入的流





DVD 输入的流作为数组的已加密的 DVD 包提供给微型驱动程序。 包是 DVD 规范中定义。 请注意因为 Microsoft 的 DVD 体系结构为音频和视频同步使用的"主时钟"模式的包的系统时钟参考 (SCR) 字段设置为零。 通常情况下，DVD 解码器微型驱动程序的音频流提供主时钟。 有关详细信息，请参阅[Master 时钟](master-clock.md)。

DVD 数据流发送到微型的驱动程序通过[ **SRB\_编写\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff568220)请求。 有关 SRB 请求的详细信息，请参阅[处理 Stream 请求块](handling-stream-request-blocks.md)并[Stream 类 SRB 引用](https://msdn.microsoft.com/library/windows/hardware/ff568295)。 硬件应支持散播-聚集 DMA，因为多个 DVD 包可能会出现在单个请求数据包。

下表介绍了使用的 DVD 电影 MPEG2 视频的输入的流媒体类型：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
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
<td><p>设置格式块说明符 GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_MPEG2_VIDEO</p></td>
</tr>
<tr class="even">
<td><p>格式块结构</p></td>
<td><p>MPEG2VIDEOINFO</p>
<div>
 
</div>
（VIDEOINFO2 结构的超集。 此外指示 MPEG 配置文件和级别。）</td>
</tr>
</tbody>
</table>

 

下表介绍了使用的 DVD 电影 ac-3 音频输入的流媒体类型：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
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
<td><p>设置格式块说明符 GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p>
<p>（请注意，这希望变化）。</p></td>
</tr>
<tr class="even">
<td><p>格式块结构</p></td>
<td><p>KSDATAFORMAT_WAVEFORMATEX</p>
<div>
 
</div>
WaveFormatEx 的超集
<p>（两个以上声道。 Down-mix 描述符。)</p></td>
</tr>
</tbody>
</table>

 

下表介绍了使用的 DVD 电影 LPCM 音频输入的流媒体类型：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
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
<td><p>设置格式块说明符 GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p></td>
</tr>
<tr class="even">
<td><p>格式块结构</p></td>
<td><p>KSDATAFORMAT_WAVEFORMATEX</p></td>
</tr>
</tbody>
</table>

 

下表介绍了使用的 DVD 电影的 DTS 音频输入的流媒体类型：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
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
<td><p>设置格式块说明符 GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p>
<p>（请注意，这希望变化）。</p></td>
</tr>
<tr class="even">
<td><p>格式块结构</p></td>
<td><p>KSDATAFORMAT_WAVEFORMATEX</p>
<div>
 
</div>
WaveFormatEx 的超集
<p>（两个以上声道。 Down-mix 描述符。)</p></td>
</tr>
</tbody>
</table>

 

下表介绍了使用的 DVD 电影 SDD 音频输入的流媒体类型：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
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
<td><p>设置格式块说明符 GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_WAVEFORMATEX</p>
<p>（请注意，这希望变化）。</p></td>
</tr>
<tr class="even">
<td><p>格式块结构</p></td>
<td><p>KSDATAFORMAT_WAVEFORMATEX</p>
<div>
 
</div>
WaveFormatEx 的超集
<p>（两个以上声道。 Down-mix 描述符。)</p></td>
</tr>
</tbody>
</table>

 

下表介绍了使用的 DVD 电影的子画面流媒体类型：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
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
<td><p>设置格式块说明符 GUID</p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NONE</p></td>
</tr>
<tr class="even">
<td><p>格式块结构</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

 

突出显示子画面，调色板信息和突出显示的信息作为属性传递。 子画面数据流包含的数据包数据，如 DVD 规范提供。 尽管包标头将剥，但仍提供。

Microsoft 在任何给定时间提供 DVD 导航器筛选器分析所有按钮和键盘的信息和仅传递到子画面解码器的一个突出显示矩形。 因此，突出显示的信息通常不是位于 DVD 流发送到解码器。 这与 DVD 规范中的不同。

DVD 拆分器导航器/筛选器处理击键的所有信息并发送新突出显示每次在按钮状态发生更改的信息。 信息描述一次只有一种模式的一个按钮。 如果存在，它会在屏幕的像素坐标或显示的子画面，包括显示矩形。 [ **KSPROPERTY\_SPHLI** ](https://msdn.microsoft.com/library/windows/hardware/ff565627)结构还包含颜色和对比的信息，但仅针对当前所选按钮的当前状态。 DVD 规范中定义的格式。

突出显示信息以异步方式到达了数据流。 DVD 解码器微型驱动程序必须使用突出显示开始和结束时间戳，以关联到相关的子画面信息中，突出显示的信息，如果有的话。 如果 DVD 解码器微型驱动程序未收到的请求的时间戳的任何子画面流信息，解码器假定将突出显示信息是独立的并且不适用于子画面。 在这种情况下，可以假定的颜色和对比的信息完全相同颜色。

突出显示的信息包含开始和结束时间戳。 以下是在同一个单位为其他时间戳，但以下两点除外：0xFFFFFFFF 开始时间戳表示突出显示属性才有效收到后，结束时间戳的 0xFFFFFFFF 表示突出显示属性有效，直到接收到的下一步的突出显示。

 

 




