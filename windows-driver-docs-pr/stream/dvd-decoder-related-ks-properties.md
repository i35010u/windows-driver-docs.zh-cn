---
title: 与 DVD 解码器相关的 KS 属性
description: 与 DVD 解码器相关的 KS 属性
ms.assetid: 97ce831e-429b-4097-a9f4-625315fe1247
keywords:
- DVD 解码器微型驱动程序 WDK，KS 属性
- 解码器微型驱动程序 WDK DVD，KS 属性
- KS 属性 WDK DVD 解码器
- 属性设置 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d411e643b80df00d3ce77c2cf334240bfdb5eb67
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106374"
---
# <a name="dvd-decoder-related-ks-properties"></a>与 DVD 解码器相关的 KS 属性





下表描述了与 DVD 解码器相关的内核流式处理属性集及其各自的属性：

[KSPROPSETID \_ AudioDecoderOut](./kspropsetid-audiodecoderout.md)属性集将所有与 DVD 解码器硬件的音频输出相关的内核流式处理属性组合在一起。

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
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-auddecout-modes" data-raw-source="[&lt;strong&gt;KSPROPERTY_AUDDECOUT_MODES&lt;/strong&gt;](./ksproperty-auddecout-modes.md)"><strong>KSPROPERTY_AUDDECOUT_MODES</strong></a></p></td>
<td><p>指定解码器硬件支持的所有潜在音频输出模式的按位组合，例如 PCM 5.1 和 S/PDIF。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-auddecout-cur-mode" data-raw-source="[&lt;strong&gt;KSPROPERTY_AUDDECOUT_CUR_MODE&lt;/strong&gt;](./ksproperty-auddecout-cur-mode.md)"><strong>KSPROPERTY_AUDDECOUT_CUR_MODE</strong></a></p></td>
<td><p>指定解码器硬件的当前音频输出模式，如立体声模拟或 S/PDIF。</p></td>
</tr>
</tbody>
</table>

 

[KSPROPSETID \_ DvdSubPic](./kspropsetid-dvdsubpic.md)属性集将所有与 DVD 子画面显示相关的内核流式处理属性组合在一起。

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
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-dvdsubpic-palette" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDSUBPIC_PALETTE&lt;/strong&gt;](./ksproperty-dvdsubpic-palette.md)"><strong>KSPROPERTY_DVDSUBPIC_PALETTE</strong></a></p></td>
<td><p>为子画面显示指定 16 YUV 调色板项。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-dvdsubpic-hli" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDSUBPIC_HLI&lt;/strong&gt;](./ksproperty-dvdsubpic-hli.md)"><strong>KSPROPERTY_DVDSUBPIC_HLI</strong></a></p></td>
<td><p>指定要更改其颜色或对比度的子画面的矩形。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-dvdsubpic-composit-on" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDSUBPIC_COMPOSIT_ON&lt;/strong&gt;](./ksproperty-dvdsubpic-composit-on.md)"><strong>KSPROPERTY_DVDSUBPIC_COMPOSIT_ON</strong></a></p></td>
<td><p>指定是启用还是禁用 DVD 子画面的显示。</p></td>
</tr>
</tbody>
</table>

 

[KSPROPSETID \_ CopyProt](./kspropsetid-copyprot.md)属性集将所有与 MACROVISION 复制保护 DVD 内容相关的内核流式处理属性组合在一起。

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
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-dvdcopy-chlg-key" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_CHLG_KEY&lt;/strong&gt;](./ksproperty-dvdcopy-chlg-key.md)"><strong>KSPROPERTY_DVDCOPY_CHLG_KEY</strong></a></p></td>
<td><p>为解码器硬件与 DVD 驱动器之间的总线质询密钥指定。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-dvdcopy-dvd-key1" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DVD_KEY1&lt;/strong&gt;](./ksproperty-dvdcopy-dvd-key1.md)"><strong>KSPROPERTY_DVDCOPY_DVD_KEY1</strong></a></p></td>
<td><p>将解码器的第一个总线密钥指定为复制保护机制的一部分。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-dvdcopy-dec-key2" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DEC_KEY2&lt;/strong&gt;](./ksproperty-dvdcopy-dec-key2.md)"><strong>KSPROPERTY_DVDCOPY_DEC_KEY2</strong></a></p></td>
<td><p>将解码器的第二个总线密钥指定为复制保护机制的一部分。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-dvdcopy-title-key" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_TITLE_KEY&lt;/strong&gt;](./ksproperty-dvdcopy-title-key.md)"><strong>KSPROPERTY_DVDCOPY_TITLE_KEY</strong></a></p></td>
<td><p>将当前 DVD 内容中的标题键指定为复制保护机制的一部分。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-copy-macrovision" data-raw-source="[&lt;strong&gt;KSPROPERTY_COPY_MACROVISION&lt;/strong&gt;](./ksproperty-copy-macrovision.md)"><strong>KSPROPERTY_COPY_MACROVISION</strong></a></p></td>
<td><p>指定数据流的 Macrovision 级别。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-dvdcopy-region" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_REGION&lt;/strong&gt;](./ksproperty-dvdcopy-region.md)"><strong>KSPROPERTY_DVDCOPY_REGION</strong></a></p></td>
<td><p>在复制保护机制中，根据语言限制指定当前区域。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-dvdcopy-set-copy-state" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_SET_COPY_STATE&lt;/strong&gt;](./ksproperty-dvdcopy-set-copy-state.md)"><strong>KSPROPERTY_DVDCOPY_SET_COPY_STATE</strong></a></p></td>
<td><p>指定硬件 DVD 解码器流的复制状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-dvdcopy-disc-key" data-raw-source="[&lt;strong&gt;KSPROPERTY_DVDCOPY_DISC_KEY&lt;/strong&gt;](./ksproperty-dvdcopy-disc-key.md)"><strong>KSPROPERTY_DVDCOPY_DISC_KEY</strong></a></p></td>
<td><p>将解码器的光盘密钥指定为复制保护机制的一部分。</p></td>
</tr>
</tbody>
</table>

 

[KSPROPSETID \_ TSRateChange](./kspropsetid-tsratechange.md)属性集对与时间戳速率更改相关的所有内核流式处理属性进行分组。

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
<td><p><a href="/windows-hardware/drivers/stream/ks-am-rate-simpleratechange" data-raw-source="[&lt;strong&gt;KS_AM_RATE_SimpleRateChange&lt;/strong&gt;](./ks-am-rate-simpleratechange.md)"><strong>KS_AM_RATE_SimpleRateChange</strong></a></p></td>
<td><p>指定开始新时间戳的开始时间。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ks-am-rate-exactratechange" data-raw-source="[&lt;strong&gt;KS_AM_RATE_ExactRateChange&lt;/strong&gt;](./ks-am-rate-exactratechange.md)"><strong>KS_AM_RATE_ExactRateChange</strong></a></p></td>
<td><p>指定一个 "输入" 时间戳以开始新的时间戳。 尚未实现此属性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ks-am-rate-maxfulldatarate" data-raw-source="[&lt;strong&gt;KS_AM_RATE_MaxFullDataRate&lt;/strong&gt;](./ks-am-rate-maxfulldatarate.md)"><strong>KS_AM_RATE_MaxFullDataRate</strong></a></p></td>
<td><p>指定最大完整数据速率。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ks-am-rate-step" data-raw-source="[&lt;strong&gt;KS_AM_RATE_Step&lt;/strong&gt;](./ks-am-rate-step.md)"><strong>KS_AM_RATE_Step</strong></a></p></td>
<td><p>尚未实现此属性。</p></td>
</tr>
</tbody>
</table>

 

[KSPROPSETID \_ VPCONFIG 和 KSPROPSETID \_ VPVBIConfig](./kspropsetid-vpconfig-and-kspropsetid-vpvbiconfig.md)属性集将与视频端口配置和视频端口垂直遮蔽间隔配置相关的所有内核流式处理属性组合在一起。 这两个属性集包含相同的属性。

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
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-vpconfig-numconnectinfo" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_NUMCONNECTINFO&lt;/strong&gt;](./ksproperty-vpconfig-numconnectinfo.md)"><strong>KSPROPERTY_VPCONFIG_NUMCONNECTINFO</strong></a></p></td>
<td><p>指定视频端口的最大连接数。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-vpconfig-getconnectinfo" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_GETCONNECTINFO&lt;/strong&gt;](./ksproperty-vpconfig-getconnectinfo.md)"><strong>KSPROPERTY_VPCONFIG_GETCONNECTINFO</strong></a></p></td>
<td><p>指定可能的视频端口配置的数组。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-vpconfig-setconnectinfo" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_SETCONNECTINFO&lt;/strong&gt;](./ksproperty-vpconfig-setconnectinfo.md)"><strong>KSPROPERTY_VPCONFIG_SETCONNECTINFO</strong></a></p></td>
<td><p>指定可能配置的数组中的特定视频端口配置。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-vpconfig-vpdatainfo" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_VPDATAINFO&lt;/strong&gt;](./ksproperty-vpconfig-vpdatainfo.md)"><strong>KSPROPERTY_VPCONFIG_VPDATAINFO</strong></a></p></td>
<td><p>指定初始视频端口配置，例如像素宽高比 r 和字段极性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-vpconfig-maxpixelrate" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_MAXPIXELRATE&lt;/strong&gt;](./ksproperty-vpconfig-maxpixelrate.md)"><strong>KSPROPERTY_VPCONFIG_MAXPIXELRATE</strong></a></p></td>
<td><p>指定具有特定维度的视频端口的最大像素速率。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-vpconfig-numvideoformat" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_NUMVIDEOFORMAT&lt;/strong&gt;](./ksproperty-vpconfig-numvideoformat.md)"><strong>KSPROPERTY_VPCONFIG_NUMVIDEOFORMAT</strong></a></p></td>
<td><p>指定像素格式的最大数目。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-vpconfig-getvideoformat" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_GETVIDEOFORMAT&lt;/strong&gt;](./ksproperty-vpconfig-getvideoformat.md)"><strong>KSPROPERTY_VPCONFIG_GETVIDEOFORMAT</strong></a></p></td>
<td><p>指定可能的像素格式的数组。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-vpconfig-setvideoformat" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_SETVIDEOFORMAT&lt;/strong&gt;](./ksproperty-vpconfig-setvideoformat.md)"><strong>KSPROPERTY_VPCONFIG_SETVIDEOFORMAT</strong></a></p></td>
<td><p>指定可能像素格式的数组中的特定像素格式。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-vpconfig-invertpolarity" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_INVERTPOLARITY&lt;/strong&gt;](./ksproperty-vpconfig-invertpolarity.md)"><strong>KSPROPERTY_VPCONFIG_INVERTPOLARITY</strong></a></p></td>
<td><p>指定是否反转视频端口的极性。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-vpconfig-decimationcapability" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY&lt;/strong&gt;](./ksproperty-vpconfig-decimationcapability.md)"><strong>KSPROPERTY_VPCONFIG_DECIMATIONCAPABILITY</strong></a></p></td>
<td><p>指定硬件是否可以减小映像大小。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-vpconfig-scalefactor" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_SCALEFACTOR&lt;/strong&gt;](./ksproperty-vpconfig-scalefactor.md)"><strong>KSPROPERTY_VPCONFIG_SCALEFACTOR</strong></a></p></td>
<td><p>指定用户定义的视频端口尺寸，包括宽度和高度。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-vpconfig-ddrawhandle" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_DDRAWHANDLE&lt;/strong&gt;](./ksproperty-vpconfig-ddrawhandle.md)"><strong>KSPROPERTY_VPCONFIG_DDRAWHANDLE</strong></a></p></td>
<td><p>指定 DirectDraw 句柄信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-vpconfig-videoportid" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_VIDEOPORTID&lt;/strong&gt;](./ksproperty-vpconfig-videoportid.md)"><strong>KSPROPERTY_VPCONFIG_VIDEOPORTID</strong></a></p></td>
<td><p>指定视频端口 ID 信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-vpconfig-ddrawsurfacehandle" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_DDRAWSURFACEHANDLE&lt;/strong&gt;](./ksproperty-vpconfig-ddrawsurfacehandle.md)"><strong>KSPROPERTY_VPCONFIG_DDRAWSURFACEHANDLE</strong></a></p></td>
<td><p>指定 DirectDraw 面控点信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-vpconfig-surfaceparams" data-raw-source="[&lt;strong&gt;KSPROPERTY_VPCONFIG_SURFACEPARAMS&lt;/strong&gt;](./ksproperty-vpconfig-surfaceparams.md)"><strong>KSPROPERTY_VPCONFIG_SURFACEPARAMS</strong></a></p></td>
<td><p>指定图面的参数，如 x 和 y 的源和间距。</p></td>
</tr>
</tbody>
</table>

 

[KSPROPSETID \_ Wave](./kspropsetid-wave.md)属性集将所有与控制 DVD 解码器硬件的输出量或具有音频循环后线的模拟电视调谐器适配器相关的内核流式处理属性组合在一起。

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
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-wave-compatible-capabilities" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_COMPATIBLE_CAPABILITIES&lt;/strong&gt;](./ksproperty-wave-compatible-capabilities.md)"><strong>KSPROPERTY_WAVE_COMPATIBLE_CAPABILITIES</strong></a></p></td>
<td><p>指定设备的波形兼容功能，例如设备是否接受输入并生成输出。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-wave-input-capabilities" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_INPUT_CAPABILITIES&lt;/strong&gt;](./ksproperty-wave-input-capabilities.md)"><strong>KSPROPERTY_WAVE_INPUT_CAPABILITIES</strong></a></p></td>
<td><p>指定设备硬件的 wave 输入功能，如采样频率和每个样本的位数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-wave-output-capabilities" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_OUTPUT_CAPABILITIES&lt;/strong&gt;](./ksproperty-wave-output-capabilities.md)"><strong>KSPROPERTY_WAVE_OUTPUT_CAPABILITIES</strong></a></p></td>
<td><p>指定设备硬件的 wave 输出功能，如每个样本的位数和可用示例内存。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-wave-buffer" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_BUFFER&lt;/strong&gt;](./ksproperty-wave-buffer.md)"><strong>KSPROPERTY_WAVE_BUFFER</strong></a></p></td>
<td><p>指定设备硬件的波形缓冲区设置，例如循环属性、波形缓冲区大小和波形缓冲区的起始地址。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-wave-frequency" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_FREQUENCY&lt;/strong&gt;](./ksproperty-wave-frequency.md)"><strong>KSPROPERTY_WAVE_FREQUENCY</strong></a></p></td>
<td><p>指定设备硬件的频率。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-wave-volume" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_VOLUME&lt;/strong&gt;](./ksproperty-wave-volume.md)"><strong>KSPROPERTY_WAVE_VOLUME</strong></a></p></td>
<td><p>指定设备硬件的左右卷衰减。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-wave-pan" data-raw-source="[&lt;strong&gt;KSPROPERTY_WAVE_PAN&lt;/strong&gt;](./ksproperty-wave-pan.md)"><strong>KSPROPERTY_WAVE_PAN</strong></a></p></td>
<td><p>指定设备硬件的左侧和右侧平移级别。</p></td>
</tr>
</tbody>
</table>

 

