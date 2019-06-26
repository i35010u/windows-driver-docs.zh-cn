---
title: 可扩展的波形格式描述符
description: 可扩展的波形格式描述符
ms.assetid: b80e651b-fb97-4502-8526-e844425805dc
keywords:
- wave 格式描述符 WDK 音频
- PCM 格式 WDK 音频
- wave 格式标记 WDK 音频
- 批流 WDK 音频
- WDK 的音频数据格式
- 数据格式以 WDK 音频，波形格式说明符
- 格式 WDK 音频，波形格式说明符
- KSDATAFORMAT 结构
- KMixer 系统驱动程序 WDK 音频，波形格式说明符
- WAVEFORMATEXTENSIBLE
- WAVEFORMATEX 结构
- WDM 音频数据格式 WDK
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28966461133ce95dc909234154b9898ef5c647ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360044"
---
# <a name="extensible-wave-format-descriptors"></a>可扩展的波形格式描述符


## <span id="extensible_wave_format_descriptors"></span><span id="EXTENSIBLE_WAVE_FORMAT_DESCRIPTORS"></span>


下图显示了波形音频流的数据格式说明符。

![说明波形格式说明符的关系图](images/wavefmt.png)

如下图所示的其他格式信息下面[ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)结构而异的数据格式。

音频系统中通过多种方式使用这种类型的格式说明符：

-   正如在上图中所示作为调用参数传递给微型端口驱动程序的格式说明符**NewStream**方法 (有关示例，请参阅[ **IMiniportWaveCyclic::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclic-newstream)).

-   *ResultantFormat*的参数[ **IMiniport::DataRangeIntersection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiport-datarangeintersection)指向缓冲区到该方法将写入一个格式说明符的方法类似于在上图中所示。

-   [ **KSPROPERTY\_PIN\_DATAINTERSECTION** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataintersection)属性 get 请求检索类似如上图所示的格式说明符。

-   [ **KSPROPERTY\_PIN\_PROPOSEDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-proposedataformat)集属性请求会接受类似如上图所示的格式说明符。

-   使用类似的格式[ **KsCreatePin** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatepin)函数的*Connect*调用参数。 此参数指向[ **KSPIN\_CONNECT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_connect)还包含一个格式说明符的缓冲区开始处的结构。 格式说明符，紧随 KSPIN\_连接结构，以在上图中所示的 KSDATAFORMAT 结构开始。

遵循 KSDATAFORMAT 结构的格式信息应[ **WAVEFORMATEXTENSIBLE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-waveformatextensible)结构或[ **WAVEFORMATEX** ](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)结构。 WAVEFORMATEXTENSIBLE 是可以描述更广泛的格式比 WAVEFORMATEX WAVEFORMATEX 的扩展的版本。 WAVEFORMATEX 是 pre WDM WAVEFORMAT 结构的扩展的版本。 WAVEFORMAT 已过时，不受任何版本的 Microsoft Windows 中的 WDM 音频子系统。

同样，PCMWAVEFORMAT 结构是的 WAVEFORMAT 已过时，但 WDM 音频子系统为其提供有限的支持的扩展的版本。

有关 WAVEFORMAT 和 PCMWAVEFORMAT 信息，请参阅 Microsoft Windows SDK 文档。

四个的波形格式结构-WAVEFORMAT、 PCMWAVEFORMAT、 WAVEFORMATEX 和 WAVEFORMATEXTENSIBLE-所有以相同的五个成员，从开始开头**wFormatTag**。 上图显示了这些其他以突出显示的是相同的结构部分上叠加的四个结构。 通过添加扩展 WAVEFORMAT PCMWAVEFORMAT 和 WAVEFORMATEX **wBitsPerSample**成员，但 WAVEFORMATEX 还将添加**cbSize**成员。 WAVEFORMATEXTENSIBLE 通过添加三个成员，从扩展 WAVEFORMATEX**示例**.wValidBitsPerSample。 (**示例**是其成员的联合**wValidSamplesPerBlock**，而不是**wValidBitsPerSample**一些压缩格式。)**WFormatTag**成员，紧随结构末尾的 KSDATAFORMAT 缓冲区中，指定何种格式信息遵循 KSDATAFORMAT。 [KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)支持仅使用下表中所示的三个格式标记之一的 PCM 格式。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">wFormatTag 值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WAVE_FORMAT_PCM</p></td>
<td align="left"><p>指定 WAVEFORMATEX 或 PCMWAVEFORMAT 整数 PCM 数据格式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WAVE_FORMAT_IEEE_FLOAT</p></td>
<td align="left"><p>指定 WAVEFORMATEX 浮点 PCM 数据格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WAVE_FORMAT_EXTENSIBLE</p></td>
<td align="left"><p>指定 WAVEFORMATEXTENSIBLE 扩展的数据格式。</p></td>
</tr>
</tbody>
</table>

 

事实上，KMixer 支持可通过这些标记值描述的 PCM 格式的一个子集 （和它支持任何非 PCM 格式）。 USB 音频设备 (请参阅[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)) 仅限于此子集，因为所有 PCM 格式的 USB 音频流都将通过 KMixer。 (某些 PCM USB 音频流可以绕过 KMixer; 有关详细信息，请参阅[USB 音频支持非 PCM 格式](usb-audio-support-for-non-pcm-formats.md)。)但是，在 Windows XP 及更早版本，DirectSound 应用程序可以通过直接连接到 WaveCyclic 和 WavePci 支持 KMixer 不支持格式的设备上的硬件 pin 来克服 KMixer 的限制。 有关详细信息，请参阅[DirectSound WDM 音频中的硬件加速](directsound-hardware-acceleration-in-wdm-audio.md)。

请注意波形的意义不明确\_格式\_PCM 标记值在上表中-它可以指定 WAVEFORMATEX 或 PCMWAVEFORMAT 结构。 但是，这些两个结构都几乎完全相同。 唯一的区别是，包含 WAVEFORMATEX **cbSize**成员和 PCMWAVEFORMAT 却没有。 根据 WAVEFORMATEX 规范**cbSize**如果，则忽略**wFormatTag** = 批\_格式\_PCM (因为**cbSize**是隐式 0)。**cbSize**用于所有其他格式。 因此，在 PCM 格式的情况下 PCMWAVEFORMAT 和 WAVEFORMATEX 包含相同的信息，可以以相同方式处理。

WAVEFORMATEX 可以指定 WAVEFORMATEXTENSIBLE 可以指定的格式的一个子集。 与 WAVEFORMATEX，不同 WAVEFORMATEXTENSIBLE 可以执行以下操作：

1.  指定的每个样本大小从单独的示例容器的位数。 例如，可以在 3 字节容器内左对齐存储 20 位示例。 WAVEFORMATEX，无法从示例容器大小区分每个样本的数据比特数，不能明确描述这种格式。

2.  将特定扬声器位置分配给多通道流中的音频声道。 WAVEFORMATEX 缺少此功能，可以充分支持仅 mono 和 （两个通道） 立体声流。

此外可以通过 WAVEFORMATEXTENSIBLE 描述由 WAVEFORMATEX 描述任何格式。 有关将 WAVEFORMATEX 结构转换为 WAVEFORMATEXTENSIBLE 的信息，请参阅[转换之间格式标记和子格式 Guid](converting-between-format-tags-and-subformat-guids.md)。

WAVEFORMATEX 足以用于描述格式，并为 8 或 16 位样本大小，但 WAVEFORMATEXTENSIBLE 进行充分描述示例精度大于 16 位格式所需。 下面是两个示例：

-   示例精度为 24 位流可以使用 32 位容器大小进行高效处理，但可以转换为使用 24 位容器来提高存储效率，而不丢失数据。

-   在处理时使用 24 位示例数据的流，提供仅 20 位精度的呈现设备可用于抖动提高其输出信号的保真度。 抖色，但是，需要额外的处理时间，并且如果原始流是精确到只有 20 位，则不需要额外的处理。

在这两个示例中，保留时的正确处理和存储效率之间权衡的信号质量有可能仅当已知示例精度和容器大小。

如果可以通过 WAVEFORMATEX 或 WAVEFORMATEXTENSIBLE 结构明确描述简单的格式，音频驱动程序已选择任一结构来描述格式的选项。 但是，音频驱动程序通常使用了 WAVEFORMATEX 的 8 位或 16 位示例指定 mono 和 （两个通道） 立体声 PCM 格式，并且某些较旧的应用程序可能希望所有的音频驱动程序以使用 WAVEFORMATEX 来指定这些格式。

如果驱动程序支持可以明确地指定为 WAVEFORMATEX 或 WAVEFORMATEXTENSIBLE 结构的音频格式，驱动程序应识别而不考虑这两个结构的客户端应用程序或组件使用指定的格式结构。 例如，如果音频设备支持的 44.1 kHz 16 位、 立体声 PCM 格式，微型端口驱动程序的 KSPROPERTY\_PIN\_PROPOSEDATAFORMAT 属性处理程序和其实现**NewStream**方法应接受该格式而不考虑是否为 WAVEFORMATEX 或 WAVEFORMATEXTENSIBLE 结构指定的格式。

若要简化格式数据的处理，驱动程序通常使用 WAVEFORMATEXTENSIBLE 结构在内部表示格式。 这种方法可能需要输入的 WAVEFORMATEX 结构转换为内部 WAVEFORMATEXTENSIBLE 表示形式或向输出 WAVEFORMATEX 结构内部 WAVEFORMATEXTENSIBLE 表示形式的转换。

从转换时的格式说明符 WAVEFORMATEX WAVEFORMATEXTENSIBLE，如果**wFormatTag** WAVEFORMATEX 结构中的成员是任一批\_格式\_PCM 或批\_格式\_IEEE\_浮动，设置**dwChannelMask**对任一演讲者 WAVEFORMATEXTENSIBLE 结构中的成员\_FRONT\_（适用于使用 mono 的流） 的中心或演讲者\_前端\_左侧 |说话人\_FRONT\_右 （对于立体声的流）。 说话人\_FRONT\_*XXX*标头文件 Ksmedia.h 中定义常量。

在除 Windows 98"黄金"所有 Windows 版本中，KMixer 支持具有多个通道，具有每个样本最多 32 位 WAVEFORMATEXTENSIBLE PCM 范围格式。

WAVEFORMATEX PCM 子集设置格式，KMixer 支持方面有何不同 Windows 版本中下, 表中所示。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows 版本</th>
<th align="left">打包的样本大小</th>
<th align="left">通道数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 98 "Gold"</p></td>
<td align="left"><p>8、 16、 24 和 32 位</p></td>
<td align="left"><p>多渠道</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 98 SE</p></td>
<td align="left"><p>8 核和 16 位</p></td>
<td align="left"><p>Mono 和立体声设备仅</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 98 SE + 修补程序</p></td>
<td align="left"><p>8、 16、 24 和 32 位</p></td>
<td align="left"><p>Mono 和立体声设备仅</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>8 核和 16 位</p></td>
<td align="left"><p>Mono 和立体声设备仅</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Me</p></td>
<td align="left"><p>8、 16、 24 和 32 位</p></td>
<td align="left"><p>Mono 和立体声设备仅</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP 及更高版本</p></td>
<td align="left"><p>8 核和 16 位</p></td>
<td align="left"><p>Mono 和立体声设备仅</p></td>
</tr>
</tbody>
</table>

 
WAVEFORMATEXTENSIBLE，在**dwBitsPerSample**容器大小，并**wValidBitsPerSample**是每个样本的有效的数据比特数。 容器是始终在内存中，字节对齐，容器大小必须指定为八位的倍数。

定义 WAVEFORMATEXTENSIBLE 结构之前，供应商必须向 Microsoft 注册的每个新一波格式，以便官方、 16 位格式标记无法分配到格式。 (格式标记包含在**wFormatTag** WAVEFORMATEX 结构中的成员。)公共标题文件 Mmreg.h 中显示的已注册的格式标记列表 (例如，WAVE\_格式\_MPEG)。

随着 WAVEFORMATEXTENSIBLE，注册格式已不再必要。 供应商独立可以将 Guid 分配给其新的格式，根据需要。 (中包含 GUID 的格式**子格式**WAVEFORMATEXTENSIBLE 的成员。)但是，Microsoft 列出了一些更受欢迎的格式中公共标题文件 Ksmedia.h 的 Guid (例如，KSDATAFORMAT\_子类型\_MPEG)。 定义一种新格式的 GUID 之前, 供应商应检查列表 KSDATAFORMAT\_子类型\_*XXX*中 Ksmedia.h 来确定适当的 GUID 是否已定义为特定的常量格式。

当使用 WAVEFORMATEXTENSIBLE，设置**wFormatTag**到批\_格式\_可扩展并**子格式**到相应格式的 GUID。 对于整数 PCM 格式设置**子格式**到 KSDATAFORMAT\_子类型\_PCM。 对于 PCM 格式进行编码以浮点数形式的示例值，设置**子格式**到 KSDATAFORMAT\_子类型\_IEEE\_FLOAT。 对于这些格式之一，设置**cbSize**到**sizeof**(WAVEFORMATEXTENSIBLE) **-sizeof**(WAVEFORMATEX)。 有关使用 WAVEFORMATEXTENSIBLE 描述非 PCM 数据格式的信息，请参阅[支持非 PCM 波形格式](supporting-non-pcm-wave-formats.md)。

 

 




