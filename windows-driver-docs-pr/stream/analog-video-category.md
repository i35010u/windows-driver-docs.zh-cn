---
title: 模拟视频类别
description: 模拟视频类别
ms.assetid: 64564c81-b1e1-482b-ae70-59b229a5e86f
keywords:
- 流类别 WDK 视频捕获，模拟视频
- 模拟视频类别 WDK 视频捕获
- PINNAME_VIDEO_ANALOGVIDEOIN
- 模拟音频 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9ad6ab2064cfc78323eac00ea43d2533310b102
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384823"
---
# <a name="analog-video-category"></a>模拟视频类别


以下 GUID 对应于类别中将模拟视频：

-   **PINNAME\_VIDEO\_ANALOGVIDEOIN**

    模拟视频中类别表示视频解码器筛选器的模拟视频输入的流。

指定时**PINNAME\_视频\_ANALOGVIDEOIN**，插针，使用下表中列出的信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DataRange 结构</strong></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567340" data-raw-source="[&lt;strong&gt;KS_DATARANGE_ANALOGVIDEO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567340)"><strong>KS_DATARANGE_ANALOGVIDEO</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>DataFormat 结构</strong></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567340" data-raw-source="[&lt;strong&gt;KS_DATARANGE_ANALOGVIDEO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567340)"><strong>KS_DATARANGE_ANALOGVIDEO</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>MajorFormat GUID</strong></p></td>
<td><p>KSDATAFORMAT_TYPE_ANALOGVIDEO</p></td>
</tr>
<tr class="even">
<td><p><strong>子设置的 GUID 格式</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_NONE</p></td>
</tr>
<tr class="odd">
<td><p><strong>说明符 GUID</strong></p></td>
<td><p>KSDATAFORMAT_SPECIFIER_ANALOGVIDEO</p></td>
</tr>
<tr class="even">
<td><p><strong>扩展标头大小</strong></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>所需的属性集</strong></p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p><strong>所需的事件集</strong></p></td>
<td><p>无</p></td>
</tr>
<tr class="odd">
<td><p><strong>DirectShow majortype</strong></p></td>
<td><p>MEDIATYPE_AnalogVideo</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>FORMAT_AnalogVideo</p></td>
</tr>
</tbody>
</table>

 

为模拟音频，如电视或广播音频定义没有特殊类别。 以模拟音频插针的值指定的设备类别时**MajorFormat**成员应为 KSDATAFORMAT\_类型\_模拟音频。 值**说明符**成员应为 KSDATAFORMAT\_说明符\_NONE 和**子类型**成员和格式设置块应设置为 KSDATAFORMAT\_子类型\_NONE。 单选音频有关的详细信息，请参阅[视频捕获设备使用广播调谐器](video-capture-devices-with-radio-tuners.md)。

尽管模拟视频流实质上是模仿模拟视频解码器的输入，它将同时充当优化信息的数据传输。 优化数据包，源于电视调谐器的筛选器，通过在的开始和结束的所有优化操作的任何干预纵横制筛选器传递。 数据数据包[ **KS\_TVTUNER\_更改\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567691)结构，其中包含国家/地区代码、 通道、 频率和模拟视频中的标准使用。

捕获筛选器必须传播到下游 VBI 编解码器 VBI 输出流的扩展标头中此优化数据包。

 

 




