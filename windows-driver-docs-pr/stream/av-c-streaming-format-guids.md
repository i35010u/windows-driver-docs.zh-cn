---
title: AV/C 流式处理格式 GUID
description: AV/C 流式处理格式 GUID
ms.assetid: 60f1fd59-e760-4be4-8990-e49628b76d15
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b7a0f6cedaec4530a958626e174c4989116b3b9
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104008"
---
# <a name="avc-streaming-format-guids"></a>AV/C 流式处理格式 GUID


## <span id="ddk_av_c_streaming_format_guids_ks"></span><span id="DDK_AV_C_STREAMING_FORMAT_GUIDS_KS"></span>


与任何内核流式处理驱动程序一样，AV/C 流式处理次级驱动程序使用格式 Guid 为每个 pin 指定它支持的数据格式范围。 然后，内核流式处理应用程序使用这些格式 Guid 来执行特定数据格式的数据范围交集。 结果为填充 [**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat) 结构。 [AVStream 中的数据范围交集](./data-range-intersections-in-avstream.md)进一步介绍了数据交集。

KSDATAFORMAT 结构指定 Guid 的主要格式、格式子类型和说明符。 说明符指定在内存中遵循 KSDATAFORMAT 结构的扩展数据结构。 例如，假设数据格式具有 KSDATAFORMAT 类型交错的主要格式 \_ \_ 、KSDATAFORMAT 子类型 DVSD 的格式子类型 \_ \_ 以及 KSDATAFORMAT \_ 说明符 DVINFO 的说明符 \_ 。 在这种情况下，扩展数据结构是 [**DVINFO**](/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_dvinfo) 结构。

*Avcstrm*头文件定义以下流格式 guid：

<span id="KSDATAFORMAT_TYPE_INTERLEAVED"></span><span id="ksdataformat_type_interleaved"></span>KSDATAFORMAT \_ 类型 \_ 交错  
指定交错的音频和视频信号。 任何包含音频的视频流都应将此 GUID 指定为流的类型。

<span id="KSDATAFORMAT_TYPE_MPEG2_TRANSPORT_STRIDE"></span><span id="ksdataformat_type_mpeg2_transport_stride"></span>KSDATAFORMAT \_ 类型 \_ MPEG2 \_ 传输 \_ 跨距  
指定偏离标准188字节 MPEG2 数据包大小的 MPEG2 流类型。 KSDATAFORMAT \_ 类型 \_ MPEG2 \_ 传输 \_ STRIDE 类型与符合 IEC 61883-4 规范的流一起使用。 这些流使用 [**MPEG2 \_ 传输 \_ STRIDE**](/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_mpeg2_transport_stride) 结构，该结构允许流描述不同于典型188字节数据包的格式。 例如，MPEG2 传输 STRIDE 的 dwOffset 成员将 \_ \_ 设置为4，将 dwPacketLength 成员设置为188，将 dwStride 成员设置为192。

<span id="KSDATAFORMAT_SUBTYPE_DVSD"></span><span id="ksdataformat_subtype_dvsd"></span>KSDATAFORMAT \_ 子类型 \_ DVSD  
指定一个 IEC 61883-2 标准定义 25-Mbps DV 信号，该信号使用用于 NTSC 信号的4:1:1 采样结构，或使用适用于 PAL 信号的4:2:0 采样结构。 此格式子类型使用 DVINFO 结构作为数据格式的扩展数据结构。

<span id="KSDATAFORMAT_SUBTYPE_DVSL"></span><span id="ksdataformat_subtype_dvsl"></span>KSDATAFORMAT \_ 子类型 \_ DVSL  
指定 IEC 61883-3 长时间运行的 12.5-Mbps DVSD 信号，该信号的行数与 NTSC 或 PAL 信号的行数相同，但是实现更高的压缩率。 此格式子类型使用 DVINFO 结构作为数据格式的扩展数据结构。

<span id="KSDATAFORMAT_SUBTYPE_DVHD"></span><span id="ksdataformat_subtype_dvhd"></span>KSDATAFORMAT \_ 子类型 \_ DVHD  
指定 IEC 61883-3 高清晰 DV 信号，如1125行 60-Hz NTSC 信号或1250线路 50-Hz PAL 信号。 当前不支持此格式子类型。

<span id="KSDATAFORMAT_SUBTYPE_DV25"></span><span id="ksdataformat_subtype_dv25"></span>KSDATAFORMAT \_ 子类型 \_ DV25  
指定一个 SMPTE 314M 25-Mbps DVCPRO 视频信号，该信号对 NTSC 和 PAL 信号使用4:1:1 采样结构。 此格式子类型使用 DVINFO 结构作为数据格式的扩展数据结构。

<span id="KSDATAFORMAT_SUBTYPE_DV50"></span><span id="ksdataformat_subtype_dv50"></span>KSDATAFORMAT \_ 子类型 \_ DV50  
指定一个 SMPTE 314M 50-Mbps DVCPRO50 视频信号，该信号对 NTSC 和 PAL 信号使用4:2:2 示例结构。 此格式子类型使用 DVINFO 结构作为数据格式的扩展数据结构。

<span id="KSDATAFORMAT_SUBTYPE_DVH1"></span><span id="ksdataformat_subtype_dvh1"></span>KSDATAFORMAT \_ 子类型 \_ DVH1  
指定 SMPTE 370M 100-Mbps 高清晰 DV 视频信号，如 720p (渐进) 或 1080i (交错) 信号。 此格式子类型使用 DVINFO 结构作为数据格式的扩展数据结构。

<span id="KSDATAFORMAT_SPECIFIER_DVINFO"></span><span id="ksdataformat_specifier_dvinfo"></span>KSDATAFORMAT \_ 说明符 \_ DVINFO  
将 DVINFO 结构指定为 KSDATAFORMAT 内存中后面的扩展数据结构。

<span id="KSDATAFORMAT_SPECIFIER_DV_AVC"></span><span id="ksdataformat_specifier_dv_avc"></span>KSDATAFORMAT \_ 说明符 \_ DV \_ AVC  
将 DVINFO 和 AVCCONNECTINFO 结构指定为在内存中执行 KSDATAFORMAT 后的扩展数据结构。

<span id="KSDATAFORMAT_SPECIFIER_AVC"></span><span id="ksdataformat_specifier_avc"></span>KSDATAFORMAT \_ 说明符 \_ AVC  
将 AVCCONNECTINFO 结构指定为 KSDATAFORMAT 内存中后面的扩展数据结构。 此说明符还可用于 MPEG2TS 格式，具体取决于格式的子类型。

<span id="KSDATAFORMAT_SPECIFIER_61883_4"></span><span id="ksdataformat_specifier_61883_4"></span>KSDATAFORMAT \_ 说明符 \_ 61883 \_ 4  
指定遵循 IEC 61883-4 协议的 MPEG2 TS 格式。 此说明符不使用任何扩展的数据结构来跟踪内存中的 KSDATAFORMAT。

### <a name="comments"></a>注释

*Avcstrm.sys* 和 *Msdv.sys* 支持 \_ windows Vista 中的 KSDATAFORMAT 子类型 \_ DV25、KSDATAFORMAT \_ 子类型 \_ DV50 和 KSDATAFORMAT \_ 子类型 \_ DVH1 格式子类型、Windows SERVER 2003 Service pack 1 (SP1) 和 windows XP service pack 2 (SP2) 操作系统。

请注意，KSDATAFORMAT \_ 子类型 \_ DVSD 和 KSDATAFORMAT \_ 子类型 \_ DV25 格式子类型与用于 NTSC 的4:1:1 采样兼容。 但是， \_ pal 格式的 KSDATAFORMAT 子类型 \_ DV25 使用4:1:1 采样 \_ ，但 PAL 格式的 KSDATAFORMAT 子类型 \_ DVSD 使用4:2:0 采样，因此，DVSD 和 DV25 之间的区别。

子单位驱动程序指示帧大小 (样本大小) 其格式子类型及其扩展数据结构的组合。 例如，KSDATAFORMAT \_ 子类型 \_ DVSD 格式子类型和 DVINFO 扩展数据结构中设置的 NTSC 位的组合指示 DV 帧大小为 120 KB。

[**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)结构包含用于验证扩展数据结构大小的**FormatSize**成员。 也就是说，在有效的扩展数据结构大小 FormatSize 等于 sizeof (KSDATAFORMAT) + sizeof (扩展数据结构 (s) # A5。

下表介绍了 KS 数据格式说明符 Guid 及其相应的扩展数据结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KS 数据格式说明符</th>
<th>扩展数据结构 (s) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSDATAFORMAT_SPECIFIER_DVINFO</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_dvinfo" data-raw-source="[&lt;strong&gt;DVINFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_dvinfo)"><strong>DVINFO</strong></a></p></td>
</tr>
<tr class="even">
<td><p>KSDATAFORMAT_SPECIFIER_DV_AVC</p></td>
<td><p>DVINFO 和<a href="/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo" data-raw-source="[&lt;strong&gt;AVCCONNECTINFO&lt;/strong&gt;](/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo)"> <strong>AVCCONNECTINFO</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>KSDATAFORMAT_SPECIFIER_AVC</p></td>
<td><p>AVCCONNECTINFO</p></td>
</tr>
<tr class="even">
<td><p>KSDATAFORMAT_SPECIFIER_61883_4</p></td>
<td><p>不使用扩展的数据结构</p></td>
</tr>
</tbody>
</table>

 

Microsoft Corporation 引入了 *msdv.sys* 的包含 WINDOWS 98 SE 的子单位驱动程序。 此驱动程序支持相机模式下的大多数 MiniDV 摄像机和 VTR (视频磁带刻录机) 模式。

Microsoft Corporation 为 Windows Me 引入了 *mstape.sys* 磁带子单位驱动程序。 此驱动程序支持 VHS 磁带卡座和 MPEG 摄像机设备。

**注意** Microsoft 不提供支持 DVCPro 格式解码的编解码器。

