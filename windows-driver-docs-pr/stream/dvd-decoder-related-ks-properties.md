---
title: 与 DVD 解码器相关的 KS 属性
description: 与 DVD 解码器相关的 KS 属性
ms.assetid: 97ce831e-429b-4097-a9f4-625315fe1247
keywords:
- DVD 解码器微型驱动程序 WDK，KS 属性
- 解码器微型驱动程序 WDK DVD，KS 属性
- KS 属性 WDK DVD 解码器
- 属性设置的 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecf271ac61821383bef130c1284271980e88f1e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363918"
---
# <a name="dvd-decoder-related-ks-properties"></a>与 DVD 解码器相关的 KS 属性





下表描述了内核流式处理属性集和相关的 DVD 解码器及其各自属性：

[KSPROPSETID\_AudioDecoderOut](https://msdn.microsoft.com/library/windows/hardware/ff566531)属性设置组流式处理音频输出与从 DVD 解码器硬件相关的属性的所有内核。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KSPROPSETID_AudioDecoderOut KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564284" data-raw-source="[&lt;strong&gt;KSPROPERTY_AUDDECOUT_MODES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564284)"><strong>KSPROPERTY_AUDDECOUT_MODES</strong></a></p></td>
<td><p>指定支持的解码器硬件，例如 PCM 5.1 和 S/PDIF 所有潜在音频输出模式的按位组合。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564283" data-raw-source="[&lt;strong&gt;KSPROPERTY_AUDDECOUT_CUR_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564283)"><strong>KSPROPERTY_AUDDECOUT_CUR_MODE</strong></a></p></td>
<td><p>指定解码器硬件，如立体声模拟或 S/PDIF 当前的音频输出的模式。</p></td>
</tr>
</tbody>
</table>

 

[KSPROPSETID\_DvdSubPic](https://msdn.microsoft.com/library/windows/hardware/ff566573)属性设置组流式处理到 DVD 子画面显示相关的属性的所有内核。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KSPROPSETID_DvdSubPic KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565151" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDSUBPIC_PALETTE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565151)"><strong>KSPROPERTY_DVDSUBPIC_PALETTE</strong></a></p></td>
<td><p>指定的子画面显示器的 16 YUV 颜色调色板条目。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565150" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDSUBPIC_HLI&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565150)"><strong>KSPROPERTY_DVDSUBPIC_HLI</strong></a></p></td>
<td><p>指定的矩形的颜色或对比度是要更改子画面。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565149" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDSUBPIC_COMPOSIT_ON&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565149)"><strong>KSPROPERTY_DVDSUBPIC_COMPOSIT_ON</strong></a></p></td>
<td><p>指定是否启用或禁用显示 DVD 子画面。</p></td>
</tr>
</tbody>
</table>

 

[KSPROPSETID\_CopyProt](https://msdn.microsoft.com/library/windows/hardware/ff566572)属性设置组流式处理与 Macrovision 的 DVD 内容复制保护相关的属性的所有内核。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KSPROPSETID_CopyProt KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565140" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_CHLG_KEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565140)"><strong>KSPROPERTY_DVDCOPY_CHLG_KEY</strong></a></p></td>
<td><p>指定解码器硬件之间的 DVD 驱动器的总线质询键。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565145" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DVD_KEY1&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565145)"><strong>KSPROPERTY_DVDCOPY_DVD_KEY1</strong></a></p></td>
<td><p>指定作为复制保护机制的一部分的解码器的第一个总线键。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565142" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DEC_KEY2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565142)"><strong>KSPROPERTY_DVDCOPY_DEC_KEY2</strong></a></p></td>
<td><p>指定作为复制保护机制的一部分的解码器的第二个总线密钥。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565148" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_TITLE_KEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565148)"><strong>KSPROPERTY_DVDCOPY_TITLE_KEY</strong></a></p></td>
<td><p>从当前 DVD 内容标题密钥指定为复制保护机制的一部分。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565114" data-raw-source="[&lt;strong&gt;KSPROPERTY_COPY_MACROVISION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565114)"><strong>KSPROPERTY_COPY_MACROVISION</strong></a></p></td>
<td><p>指定数据流的 Macrovision 级别。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565146" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_REGION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565146)"><strong>KSPROPERTY_DVDCOPY_REGION</strong></a></p></td>
<td><p>作为复制保护机制的一部分指定根据语言限制的当前区域。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565147" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_SET_COPY_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565147)"><strong>KSPROPERTY_DVDCOPY_SET_COPY_STATE</strong></a></p></td>
<td><p>指定硬件 DVD 解码器的流的副本状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565144" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DISC_KEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565144)"><strong>KSPROPERTY_DVDCOPY_DISC_KEY</strong></a></p></td>
<td><p>指定作为复制保护机制的一部分的解码器的光盘密钥。</p></td>
</tr>
</tbody>
</table>

 

[KSPROPSETID\_TSRateChange](https://msdn.microsoft.com/library/windows/hardware/ff566700)属性设置组流式处理与时间戳速率更改相关的属性的所有内核。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KSPROPSETID_TSRateChange KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567288" data-raw-source="[&lt;strong&gt;KS_AM_RATE_SimpleRateChange&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567288)"><strong>KS_AM_RATE_SimpleRateChange</strong></a></p></td>
<td><p>指定的开始时间开始新的时间戳速率。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567280" data-raw-source="[&lt;strong&gt;KS_AM_RATE_ExactRateChange&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567280)"><strong>KS_AM_RATE_ExactRateChange</strong></a></p></td>
<td><p>指定"输入"时间戳，以开始新的时间戳率。 此属性尚未实现。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567284" data-raw-source="[&lt;strong&gt;KS_AM_RATE_MaxFullDataRate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567284)"><strong>KS_AM_RATE_MaxFullDataRate</strong></a></p></td>
<td><p>指定的最大的完整数据速率。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567289" data-raw-source="[&lt;strong&gt;KS_AM_RATE_Step&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567289)"><strong>KS_AM_RATE_Step</strong></a></p></td>
<td><p>此属性尚未实现。</p></td>
</tr>
</tbody>
</table>

 

[KSPROPSETID\_VPConfig 和 KSPROPSETID\_VPVBIConfig](https://msdn.microsoft.com/library/windows/hardware/ff566703)属性集组流式处理与视频端口配置和视频端口消隐相关的属性的所有内核配置。 这两个属性集包含相同的属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KSPROPSETID_VPConfig 和 KSPROPSETID_VPVBIConfig KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566497" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_NUMCONNECTINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566497)"><strong>KSPROPERTY_VPCONFIG_NUMCONNECTINFO</strong></a></p></td>
<td><p>指定的最大的视频端口到电气连接数。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566483" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_GETCONNECTINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566483)"><strong>KSPROPERTY_VPCONFIG_GETCONNECTINFO</strong></a></p></td>
<td><p>指定可能的视频端口配置一个数组。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566504" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_SETCONNECTINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566504)"><strong>KSPROPERTY_VPCONFIG_SETCONNECTINFO</strong></a></p></td>
<td><p>指定数组中的可能的配置的特定视频端口配置。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566513" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_VPDATAINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566513)"><strong>KSPROPERTY_VPCONFIG_VPDATAINFO</strong></a></p></td>
<td><p>指定的初始的视频端口配置，如像素方面定量供应和字段极性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566494" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_MAXPIXELRATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566494)"><strong>KSPROPERTY_VPCONFIG_MAXPIXELRATE</strong></a></p></td>
<td><p>指定与特定维度的最大像素率的视频端口。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566500" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_NUMVIDEOFORMAT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566500)"><strong>KSPROPERTY_VPCONFIG_NUMVIDEOFORMAT</strong></a></p></td>
<td><p>指定像素格式的最大数目。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566485" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_GETVIDEOFORMAT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566485)"><strong>KSPROPERTY_VPCONFIG_GETVIDEOFORMAT</strong></a></p></td>
<td><p>指定的可能的像素格式的数组。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566506" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_SETVIDEOFORMAT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566506)"><strong>KSPROPERTY_VPCONFIG_SETVIDEOFORMAT</strong></a></p></td>
<td><p>指定可能的像素格式的数组从特定的像素格式...</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566487" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_INVERTPOLARITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566487)"><strong>KSPROPERTY_VPCONFIG_INVERTPOLARITY</strong></a></p></td>
<td><p>指定是否反转极性的视频端口。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566478" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566478)"><strong>KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY</strong></a></p></td>
<td><p>指定是否在硬件可以减小映像大小。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566502" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_SCALEFACTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566502)"><strong>KSPROPERTY_VPCONFIG_SCALEFACTOR</strong></a></p></td>
<td><p>指定用户定义的视频端口维度，包括宽度和高度。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566101" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_DDRAWHANDLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566101)"><strong>KSPROPERTY_VPCONFIG_DDRAWHANDLE</strong></a></p></td>
<td><p>指定 DirectDraw 句柄的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566511" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_VIDEOPORTID&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566511)"><strong>KSPROPERTY_VPCONFIG_VIDEOPORTID</strong></a></p></td>
<td><p>指定的视频端口 ID 信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566471" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_DDRAWSURFACEHANDLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566471)"><strong>KSPROPERTY_VPCONFIG_DDRAWSURFACEHANDLE</strong></a></p></td>
<td><p>指定 DirectDraw 图面上的句柄的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566509" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_SURFACEPARAMS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566509)"><strong>KSPROPERTY_VPCONFIG_SURFACEPARAMS</strong></a></p></td>
<td><p>指定的图面上的参数，例如 x 和 y 的原始信息和间距的图面。</p></td>
</tr>
</tbody>
</table>

 

[KSPROPSETID\_批](https://msdn.microsoft.com/library/windows/hardware/ff566715)属性设置组流式处理与控制的 DVD 解码器硬件或拥有音频环回电缆连接到的模拟电视调谐器适配器输出量相关的属性的所有内核一种声音适配器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KSPROPSETID_Wave KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566516" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_COMPATIBLE_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566516)"><strong>KSPROPERTY_WAVE_COMPATIBLE_CAPABILITIES</strong></a></p></td>
<td><p>指定设备的批兼容的功能，例如设备是否接受输入并生成输出。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566521" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_INPUT_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566521)"><strong>KSPROPERTY_WAVE_INPUT_CAPABILITIES</strong></a></p></td>
<td><p>指定设备硬件，如采样频率和每个样本位数的批输入的的功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566523" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_OUTPUT_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566523)"><strong>KSPROPERTY_WAVE_OUTPUT_CAPABILITIES</strong></a></p></td>
<td><p>指定设备硬件，如每个示例和内存可用示例的位的 wave 输出的功能。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566514" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_BUFFER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566514)"><strong>KSPROPERTY_WAVE_BUFFER</strong></a></p></td>
<td><p>指定设备硬件，例如循环属性、 批缓冲区大小和批缓冲区的起始地址的批缓冲区的设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566519" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_FREQUENCY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566519)"><strong>KSPROPERTY_WAVE_FREQUENCY</strong></a></p></td>
<td><p>指定设备硬件的频率。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566529" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_VOLUME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566529)"><strong>KSPROPERTY_WAVE_VOLUME</strong></a></p></td>
<td><p>指定设备硬件的左侧和右侧卷衰减。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566526" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_PAN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566526)"><strong>KSPROPERTY_WAVE_PAN</strong></a></p></td>
<td><p>指定左侧和右侧平移的设备硬件级别。</p></td>
</tr>
</tbody>
</table>

 

 

 




