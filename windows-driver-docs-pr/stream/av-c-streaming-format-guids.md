---
title: AV/C 流式处理格式 GUID
description: AV/C 流式处理格式 GUID
ms.assetid: 60f1fd59-e760-4be4-8990-e49628b76d15
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e0244c82c232fd6d4f20b0b1973b7a7b3f1ffc7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566273"
---
# <a name="avc-streaming-format-guids"></a>AV/C 流式处理格式 GUID


## <span id="ddk_av_c_streaming_format_guids_ks"></span><span id="DDK_AV_C_STREAMING_FORMAT_GUIDS_KS"></span>


任何流式处理驱动程序的内核，如 AV/C 流式处理子单元驱动程序指定的每个 pin 支持通过使用 Guid 格式的数据格式的范围。 内核流式处理应用程序然后使用这些格式的 Guid 来执行数据范围交集为特定的数据格式。 结果是一个填充接[ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)结构。 中进一步介绍了数据交集[AVStream 中的数据范围交集](https://msdn.microsoft.com/library/windows/hardware/ff558680)。

KSDATAFORMAT 结构的主要格式、 格式子类型和说明符指定 Guid。 说明符指定遵循 KSDATAFORMAT 结构在内存中的扩展数据结构。 例如，假设数据格式有的主要格式为 KSDATAFORMAT\_类型\_交叉存取 KSDATAFORMAT 的子格式类型\_子类型\_DVSD，和 KSDATAFORMAT 说明符\_说明符\_DVINFO。 在这种情况下，则扩展数据结构[ **DVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff559517)结构。

*Avcstrm.h*标头文件定义以下流式处理格式的 Guid:

<span id="KSDATAFORMAT_TYPE_INTERLEAVED"></span><span id="ksdataformat_type_interleaved"></span>KSDATAFORMAT\_类型\_交叉存取  
将指定的交错的音频和视频信号。 任何包含音频的视频流应指定此 GUID 作为流的类型。

<span id="KSDATAFORMAT_TYPE_MPEG2_TRANSPORT_STRIDE"></span><span id="ksdataformat_type_mpeg2_transport_stride"></span>KSDATAFORMAT\_TYPE\_MPEG2\_TRANSPORT\_STRIDE  
将指定偏离正常 188 字节 MPEG2 数据包大小 MPEG2 流类型。 KSDATAFORMAT\_类型\_MPEG2\_传输\_STRIDE 类型用于符合 IEC 61883 4 规范的流。 这些流使用[ **MPEG2\_传输\_STRIDE** ](https://msdn.microsoft.com/library/windows/hardware/ff567742)结构，它允许将流来描述不同于典型 188 字节数据包的格式。 例如，MPEG2 dwOffset 成员\_传输\_STRIDE 将设置为 4，到 188，dwPacketLength 成员和 192 dwStride 成员。

<span id="KSDATAFORMAT_SUBTYPE_DVSD"></span><span id="ksdataformat_subtype_dvsd"></span>KSDATAFORMAT\_SUBTYPE\_DVSD  
指定 IEC 61883 2 标准定义 25 Mbps DV 信号，使用 4:1:1 个采样结构 NTSC 信号或，使用 4:2:0 PAL 采样结构发出信号。 此格式的子类型作为数据格式的扩展数据结构使用 DVINFO 结构。

<span id="KSDATAFORMAT_SUBTYPE_DVSL"></span><span id="ksdataformat_subtype_dvsl"></span>KSDATAFORMAT\_SUBTYPE\_DVSL  
指定 IEC 61883 3 长时间播放 12.5 Mbps DVSD 信号，具有相同数量的行作为 NTSC 或 PAL 信号，但实现更高的压缩率。 此格式的子类型作为数据格式的扩展数据结构使用 DVINFO 结构。

<span id="KSDATAFORMAT_SUBTYPE_DVHD"></span><span id="ksdataformat_subtype_dvhd"></span>KSDATAFORMAT\_SUBTYPE\_DVHD  
将指定的 IEC 61883 3 高清晰度 DV 信号，例如 1125年行 60 Hz NTSC 信号或 1250年行 50 Hz PAL 信号。 目前不支持此格式的子类型。

<span id="KSDATAFORMAT_SUBTYPE_DV25"></span><span id="ksdataformat_subtype_dv25"></span>KSDATAFORMAT\_SUBTYPE\_DV25  
指定 SMPTE 314 M 25 Mbps DVCPRO 视频信号，使用 4:1:1 采样结构 NTSC 或 PAL 信号。 此格式的子类型作为数据格式的扩展数据结构使用 DVINFO 结构。

<span id="KSDATAFORMAT_SUBTYPE_DV50"></span><span id="ksdataformat_subtype_dv50"></span>KSDATAFORMAT\_子类型\_DV50  
指定 SMPTE 314 M 50 Mbps DVCPRO50 视频信号，使用 4:2:2 NTSC 或 PAL 信号的示例结构。 此格式的子类型作为数据格式的扩展数据结构使用 DVINFO 结构。

<span id="KSDATAFORMAT_SUBTYPE_DVH1"></span><span id="ksdataformat_subtype_dvh1"></span>KSDATAFORMAT\_SUBTYPE\_DVH1  
指定 SMPTE 370 M 100-Mbps 的高清 DV 视频信号，例如 720p （渐进式） 或 1080i （交错） 信号。 此格式的子类型作为数据格式的扩展数据结构使用 DVINFO 结构。

<span id="KSDATAFORMAT_SPECIFIER_DVINFO"></span><span id="ksdataformat_specifier_dvinfo"></span>KSDATAFORMAT\_SPECIFIER\_DVINFO  
将 DVINFO 结构指定为以下 KSDATAFORMAT 在内存中的扩展数据结构。

<span id="KSDATAFORMAT_SPECIFIER_DV_AVC"></span><span id="ksdataformat_specifier_dv_avc"></span>KSDATAFORMAT\_SPECIFIER\_DV\_AVC  
将在 DVINFO 和 AVCCONNECTINFO 结构指定为以下 KSDATAFORMAT 在内存中的扩展数据结构。

<span id="KSDATAFORMAT_SPECIFIER_AVC"></span><span id="ksdataformat_specifier_avc"></span>KSDATAFORMAT\_SPECIFIER\_AVC  
将 AVCCONNECTINFO 结构指定为以下 KSDATAFORMAT 在内存中的扩展数据结构。 MPEG2TS 格式，具体取决于该格式的子类型，可能还使用此说明符。

<span id="KSDATAFORMAT_SPECIFIER_61883_4"></span><span id="ksdataformat_specifier_61883_4"></span>KSDATAFORMAT\_SPECIFIER\_61883\_4  
指定 MPEG2-TS 格式都符合 IEC 61883 4 协议。 此说明符不使用任何扩展的数据结构来按照 KSDATAFORMAT 在内存中。

### <a name="comments"></a>备注

*Avcstrm.sys*并*Msdv.sys*支持 KSDATAFORMAT\_子类型\_DV25、 KSDATAFORMAT\_子类型\_DV50 和 KSDATAFORMAT\_子类型\_DVH1 格式在 Windows Vista、 Windows Server 2003 Service Pack 1 (SP1) 和 Windows XP Service Pack 2 (SP2) 操作系统中的子类型。

请注意，KSDATAFORMAT\_子类型\_DVSD 和 KSDATAFORMAT\_子类型\_DV25 格式子类型都兼容使用 4: NTSC 的 1 对 1 采样。 但是，KSDATAFORMAT\_子类型\_DV25 PAL 格式使用 4:1:1 采样但 KSDATAFORMAT\_子类型\_DVSD PAL 格式使用 4:2:0，因此采样 DVSD 和 DV25 之间的区别。

子单元驱动程序通过其格式的子类型和其扩展数据结构的组合指示的帧大小 （示例大小）。 例如，KSDATAFORMAT 的组合\_子类型\_DVSD 格式子类型和 DVINFO 扩展数据结构中设置的 NTSC 位指示的 DV 帧大小为 120 KB。

[ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)结构包含**FormatSize**用于验证的扩展数据结构大小的成员。 它是有效的扩展数据结构大小 FormatSize 等于 sizeof(KSDATAFORMAT) + sizeof (扩展数据 structure(s))。

下表介绍 KS 数据的格式说明符 Guid 和其对应的扩展数据结构。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559517" data-raw-source="[&lt;strong&gt;DVINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559517)"><strong>DVINFO</strong></a></p></td>
</tr>
<tr class="even">
<td><p>KSDATAFORMAT_SPECIFIER_DV_AVC</p></td>
<td><p>DVINFO 并<a href="https://msdn.microsoft.com/library/windows/hardware/ff554101" data-raw-source="[&lt;strong&gt;AVCCONNECTINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554101)"> <strong>AVCCONNECTINFO</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>KSDATAFORMAT_SPECIFIER_AVC</p></td>
<td><p>AVCCONNECTINFO</p></td>
</tr>
<tr class="even">
<td><p>KSDATAFORMAT_SPECIFIER_61883_4</p></td>
<td><p>不使用任何扩展的数据结构</p></td>
</tr>
</tbody>
</table>

 

Microsoft Corporation 引入*msdv.sys*子单元驱动程序和 Windows 98 SE。 此驱动程序支持大多数 MiniDV 摄像机相机模式和 VTR （视频磁带记录器） 模式。

Microsoft Corporation 引入*mstape.sys*磁带子单元驱动程序和 Windows me 一起提供。 此驱动程序支持 D VHS 磁带卡片组和 MPEG 摄像机设备。

**请注意**Microsoft 不提供支持 DVCPro 格式解码的编解码器。

 

 





