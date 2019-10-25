---
title: AV/C 流式处理格式 GUID
description: AV/C 流式处理格式 GUID
ms.assetid: 60f1fd59-e760-4be4-8990-e49628b76d15
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bd11aa78568557bb2e39ae2a07054e163034d4d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845580"
---
# <a name="avc-streaming-format-guids"></a>AV/C 流式处理格式 GUID


## <span id="ddk_av_c_streaming_format_guids_ks"></span><span id="DDK_AV_C_STREAMING_FORMAT_GUIDS_KS"></span>


与任何内核流式处理驱动程序一样，AV/C 流式处理次级驱动程序使用格式 Guid 为每个 pin 指定它支持的数据格式范围。 然后，内核流式处理应用程序使用这些格式 Guid 来执行特定数据格式的数据范围交集。 结果为填充[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)结构。 [AVStream 中的数据范围交集](https://docs.microsoft.com/windows-hardware/drivers/stream/data-range-intersections-in-avstream)进一步介绍了数据交集。

KSDATAFORMAT 结构指定 Guid 的主要格式、格式子类型和说明符。 说明符指定在内存中遵循 KSDATAFORMAT 结构的扩展数据结构。 例如，假设数据格式的主要格式为 KSDATAFORMAT\_类型\_交错、KSDATAFORMAT\_子类型的格式子类型\_DVSD 和 KSDATAFORMAT\_说明符的说明符\_DVINFO。 在这种情况下，扩展数据结构是[**DVINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_dvinfo)结构。

*Avcstrm*头文件定义以下流格式 guid：

<span id="KSDATAFORMAT_TYPE_INTERLEAVED"></span><span id="ksdataformat_type_interleaved"></span>KSDATAFORMAT\_类型\_交错  
指定交错的音频和视频信号。 任何包含音频的视频流都应将此 GUID 指定为流的类型。

<span id="KSDATAFORMAT_TYPE_MPEG2_TRANSPORT_STRIDE"></span><span id="ksdataformat_type_mpeg2_transport_stride"></span>KSDATAFORMAT\_类型\_MPEG2\_传输\_步幅  
指定偏离标准188字节 MPEG2 数据包大小的 MPEG2 流类型。 KSDATAFORMAT\_类型\_MPEG2\_传输\_步幅类型与符合 IEC 61883-4 规范的流一起使用。 这些流使用[**MPEG2\_传输\_步幅**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_mpeg2_transport_stride)结构，该结构允许流描述不同于典型188字节数据包的格式。 例如，MPEG2\_传输\_步幅的 dwOffset 成员将设置为4，将 dwPacketLength 成员设置为188，将 dwStride 成员设置为192。

<span id="KSDATAFORMAT_SUBTYPE_DVSD"></span><span id="ksdataformat_subtype_dvsd"></span>KSDATAFORMAT\_DVSD\_子类型  
指定一个 IEC 61883-2 标准定义 25-Mbps DV 信号，该信号使用用于 NTSC 信号的4:1:1 采样结构，或使用适用于 PAL 信号的4:2:0 采样结构。 此格式子类型使用 DVINFO 结构作为数据格式的扩展数据结构。

<span id="KSDATAFORMAT_SUBTYPE_DVSL"></span><span id="ksdataformat_subtype_dvsl"></span>KSDATAFORMAT\_DVSL\_子类型  
指定 IEC 61883-3 长时间运行的 12.5-Mbps DVSD 信号，该信号的行数与 NTSC 或 PAL 信号的行数相同，但是实现更高的压缩率。 此格式子类型使用 DVINFO 结构作为数据格式的扩展数据结构。

<span id="KSDATAFORMAT_SUBTYPE_DVHD"></span><span id="ksdataformat_subtype_dvhd"></span>KSDATAFORMAT\_DVHD\_子类型  
指定 IEC 61883-3 高清晰 DV 信号，如1125行 60-Hz NTSC 信号或1250线路 50-Hz PAL 信号。 当前不支持此格式子类型。

<span id="KSDATAFORMAT_SUBTYPE_DV25"></span><span id="ksdataformat_subtype_dv25"></span>KSDATAFORMAT\_DV25\_子类型  
指定一个 SMPTE 314M 25-Mbps DVCPRO 视频信号，该信号对 NTSC 和 PAL 信号使用4:1:1 采样结构。 此格式子类型使用 DVINFO 结构作为数据格式的扩展数据结构。

<span id="KSDATAFORMAT_SUBTYPE_DV50"></span><span id="ksdataformat_subtype_dv50"></span>KSDATAFORMAT\_DV50\_子类型  
指定一个 SMPTE 314M 50-Mbps DVCPRO50 视频信号，该信号对 NTSC 和 PAL 信号使用4:2:2 示例结构。 此格式子类型使用 DVINFO 结构作为数据格式的扩展数据结构。

<span id="KSDATAFORMAT_SUBTYPE_DVH1"></span><span id="ksdataformat_subtype_dvh1"></span>KSDATAFORMAT\_DVH1\_子类型  
指定 SMPTE 370M 100-Mbps 高清晰 DV 视频信号，如720p （渐进式）或1080i （交错）信号。 此格式子类型使用 DVINFO 结构作为数据格式的扩展数据结构。

<span id="KSDATAFORMAT_SPECIFIER_DVINFO"></span><span id="ksdataformat_specifier_dvinfo"></span>KSDATAFORMAT\_DVINFO\_说明符  
将 DVINFO 结构指定为 KSDATAFORMAT 内存中后面的扩展数据结构。

<span id="KSDATAFORMAT_SPECIFIER_DV_AVC"></span><span id="ksdataformat_specifier_dv_avc"></span>KSDATAFORMAT\_说明符\_DV\_AVC  
将 DVINFO 和 AVCCONNECTINFO 结构指定为在内存中执行 KSDATAFORMAT 后的扩展数据结构。

<span id="KSDATAFORMAT_SPECIFIER_AVC"></span><span id="ksdataformat_specifier_avc"></span>KSDATAFORMAT\_AVC\_说明符  
将 AVCCONNECTINFO 结构指定为 KSDATAFORMAT 内存中后面的扩展数据结构。 此说明符还可用于 MPEG2TS 格式，具体取决于格式的子类型。

<span id="KSDATAFORMAT_SPECIFIER_61883_4"></span><span id="ksdataformat_specifier_61883_4"></span>KSDATAFORMAT\_说明符\_61883\_4  
指定遵循 IEC 61883-4 协议的 MPEG2 TS 格式。 此说明符不使用任何扩展的数据结构来跟踪内存中的 KSDATAFORMAT。

### <a name="comments"></a>备注

*Avcstrm*和*Msdv*支持 KSDATAFORMAT\_子类型\_DV25、KSDATAFORMAT\_子类型\_DV50 和 KSDATAFORMAT\_子类型\_WINDOWS Vista 中的 DVH1 格式子类型，windows Server 2003Service Pack 1 （SP1）和带有 Service Pack 2 （SP2）的 Windows XP 操作系统。

请注意，KSDATAFORMAT\_子类型\_DVSD 和 KSDATAFORMAT\_子类型\_DV25 格式子类型将使用4:1:1 的 NTSC 采样进行兼容。 不过，对于 PAL 格式，KSDATAFORMAT\_子类型\_DV25 使用4:1:1 采样，但 KSDATAFORMAT\_子类型\_用于 PAL 格式的 DVSD 使用4:2:0 采样，因此在 DVSD 和 DV25 之间进行区分。

子单位驱动程序通过其格式子类型及其扩展数据结构的组合指示帧大小（示例大小）。 例如，KSDATAFORMAT\_子类型\_DVSD 格式子类型和 DVINFO 扩展数据结构中设置的 NTSC 位的组合指示 DV 帧大小为 120 KB。

[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)结构包含用于验证扩展数据结构大小的**FormatSize**成员。 也就是说，在有效的扩展数据结构大小 FormatSize 等于 sizeof （KSDATAFORMAT） + sizeof （扩展数据结构）中。

下表介绍了 KS 数据格式说明符 Guid 及其相应的扩展数据结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KS 数据格式说明符</th>
<th>扩展数据结构</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSDATAFORMAT_SPECIFIER_DVINFO</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_dvinfo" data-raw-source="[&lt;strong&gt;DVINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/avcstrm/ns-avcstrm-_dvinfo)"><strong>DVINFO</strong></a></p></td>
</tr>
<tr class="even">
<td><p>KSDATAFORMAT_SPECIFIER_DV_AVC</p></td>
<td><p>DVINFO 和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo" data-raw-source="[&lt;strong&gt;AVCCONNECTINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo)"> <strong>AVCCONNECTINFO</strong></a></p></td>
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

 

Microsoft Corporation 向 Windows 98 SE 引入了*msdv*子的驱动程序。 此驱动程序支持在摄像机模式和 VTR （视频磁带录制器）模式下的大多数 MiniDV 摄像机。

Microsoft Corporation 在 Windows Me 中引入了*mstape*磁带子单位驱动程序。 此驱动程序支持 VHS 磁带卡座和 MPEG 摄像机设备。

**注意**Microsoft 不提供支持 DVCPro 格式解码的编解码器。

 

 





