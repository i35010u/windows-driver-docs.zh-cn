---
title: 可扩展的波形格式描述符
description: 可扩展的波形格式描述符
ms.assetid: b80e651b-fb97-4502-8526-e844425805dc
keywords:
- 波形格式描述符 WDK 音频
- PCM 音频格式
- 波形格式标记 WDK 音频
- 波形流 WDK 音频
- 音频数据格式 WDK
- 数据格式化 WDK 音频，波形格式说明符
- 格式化 WDK 音频、波形格式说明符
- KSDATAFORMAT 结构
- KMixer 系统驱动程序 WDK 音频，波形格式描述符
- WAVEFORMATEXTENSIBLE
- WAVEFORMATEX 结构
- WDM 音频数据格式 WDK
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52a40b01fcecca20c423dd07bd0644ba315fed6c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831242"
---
# <a name="extensible-wave-format-descriptors"></a>可扩展的波形格式描述符


## <span id="extensible_wave_format_descriptors"></span><span id="EXTENSIBLE_WAVE_FORMAT_DESCRIPTORS"></span>


下图显示了波形音频流的数据格式说明符。

![说明波形格式说明符的关系图](images/wavefmt.png)

如图所示，根据数据格式， [**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)结构后面的附加格式信息量会有所不同。

音频系统通过多种方式使用这种类型的格式描述符：

-   如上图中所示的格式描述符将作为调用参数传递给微型端口驱动程序的**newstream.ischecked**方法（例如，请参阅[**IMiniportWaveCyclic：： newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-newstream)）。

-   [**IMiniport：:D atarangeintersection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection)方法的*ResultantFormat*参数指向一个缓冲区，此方法会将格式说明符写入其中，如上图中所示。

-   [**KSPROPERTY\_引脚\_DATAINTERSECTION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataintersection)请求检索格式描述符，如上图中所示。

-   [**KSPROPERTY\_引脚\_PROPOSEDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-proposedataformat)请求接受格式说明符，如上图中所示。

-   [**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)函数的*Connect*调用参数使用类似的格式。 此参数指向包含格式说明符的缓冲区开头的[**KSPIN\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect)结构。 紧跟在 KSPIN\_连接结构后面的格式说明符以 KSDATAFORMAT 结构开始，如上图中所示。

KSDATAFORMAT 结构后面的格式信息应为[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)结构或[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)结构。 WAVEFORMATEXTENSIBLE 是 WAVEFORMATEX 的扩展版本，可描述比 WAVEFORMATEX 更广泛的格式范围。 WAVEFORMATEX 是预 WDM WAVEFORMAT 结构的扩展版本。 WAVEFORMAT 已过时，并且任何 Microsoft Windows 版本中的 WDM 音频子系统都不支持。

同样，PCMWAVEFORMAT 结构是已过时的 WAVEFORMAT 的扩展版本，但 WDM 音频子系统提供有限的支持。

有关 WAVEFORMAT 和 PCMWAVEFORMAT 的信息，请参阅 Microsoft Windows SDK 文档。

四个波形格式结构--WAVEFORMAT、PCMWAVEFORMAT、WAVEFORMATEX 和 WAVEFORMATEXTENSIBLE--都以从**wFormatTag**开始的相同的五个成员开头。 上图显示了这四个结构彼此重叠，以突出显示完全相同的结构部分。 PCMWAVEFORMAT 和 WAVEFORMATEX 通过添加**wBitsPerSample**成员扩展 WAVEFORMAT，但 WAVEFORMATEX 还添加**cbSize**成员。 WAVEFORMATEXTENSIBLE 通过添加三个成员，从 wValidBitsPerSample 开始扩展**WAVEFORMATEX。** （**示例**是使用其他成员**wValidSamplesPerBlock**，而不是**wValidBitsPerSample**来表示某些压缩格式的联合。）紧跟在缓冲区中 KSDATAFORMAT 结构末尾的**wFormatTag**成员指定 KSDATAFORMAT 后的格式信息类型。 [KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)仅支持使用下表中所示的三种格式标记之一的 PCM 格式。

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
<td align="left"><p>WAVEFORMATEX 或 PCMWAVEFORMAT 指定的整数 PCM 数据格式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WAVE_FORMAT_IEEE_FLOAT</p></td>
<td align="left"><p>WAVEFORMATEX 指定的浮点 PCM 数据格式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WAVE_FORMAT_EXTENSIBLE</p></td>
<td align="left"><p>WAVEFORMATEXTENSIBLE 指定的扩展数据格式。</p></td>
</tr>
</tbody>
</table>

 

事实上，KMixer 仅支持可通过这些标记值描述的 PCM 格式的子集（并且它不支持非 PCM 格式）。 USB 音频设备（请参阅[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)）限制为此子集，因为所有 PCM 格式的 u 音频流都通过 KMixer。 （某些非 PCM USB 音频流可以绕过 KMixer; 有关详细信息，请参阅[非 PCM 格式的 USB 音频支持](usb-audio-support-for-non-pcm-formats.md)。）但是，在 Windows XP 及更早版本中，DirectSound 应用程序可以直接连接到 WaveCyclic 和 WavePci 设备上的硬件 pin，而和设备上不支持 KMixer。 有关详细信息，请参阅[DirectSound 硬件加速 IN WDM 音频](directsound-hardware-acceleration-in-wdm-audio.md)。

请注意，在上表中\_PCM 标记值时，波形\_格式的歧义，它可以指定 WAVEFORMATEX 或 PCMWAVEFORMAT 结构。 但是，这两个结构几乎完全相同。 唯一的区别是，WAVEFORMATEX 包含**cbSize**成员，而 PCMWAVEFORMAT 不包含。 根据 WAVEFORMATEX 规范，如果**wFormatTag** = WAVE\_格式\_PCM （因为**cbSize**隐式为零），则将忽略**cbSize** ;**cbSize**用于所有其他格式。 因此，在使用 PCM 格式的情况下，PCMWAVEFORMAT 和 WAVEFORMATEX 包含相同的信息，并且可以视为相同的信息。

WAVEFORMATEX 只能指定 WAVEFORMATEXTENSIBLE 可以指定的格式的子集。 与 WAVEFORMATEX 不同，WAVEFORMATEXTENSIBLE 可以执行以下操作：

1.  将每个样本的位数分别指定为样本容器的大小。 例如，可以在三个字节的容器内将一个20位的示例存储为左对齐。 WAVEFORMATEX 无法区分样本容器大小的每个样本的数据位数，无法明确地描述此类格式。

2.  将特定扬声器位置分配给多通道流中的音频通道。 WAVEFORMATEX 缺少此功能，只能支持单声道和（双通道）立体声流。

WAVEFORMATEX 描述的任何格式也可以通过 WAVEFORMATEXTENSIBLE 说明。 有关将 WAVEFORMATEX 结构转换为 WAVEFORMATEXTENSIBLE 的信息，请参阅[在格式标记和 Subformat Guid 之间转换](converting-between-format-tags-and-subformat-guids.md)。

WAVEFORMATEX 足以描述大小为8或16位的示例格式，但必须使用 WAVEFORMATEXTENSIBLE 来充分描述样本精度大于16位的格式。 下面是两个示例：

-   采样精度为24位的流可以使用32位容器大小来有效处理，但可转换为使用24位容器来提高存储效率，而不会丢失数据。

-   处理包含24位样本数据的流时，仅提供20位精度的渲染设备可以使用仿色来改善其输出信号的保真度。 但是，仿色需要额外的处理时间，如果原始流精确到仅20位，则不需要进行额外的处理。

在这两个示例中，仅当样本精度和容器大小都已知时，才可以在处理和存储效率之间进行适当权衡时保留信号质量。

如果 WAVEFORMATEX 或 WAVEFORMATEXTENSIBLE 结构可以明确描述简单格式，则音频驱动程序可以选择使用任一结构来描述格式。 但是，音频驱动程序通常使用 WAVEFORMATEX 来指定带有8位或16位样本的 mono 和（双通道）立体声 PCM 格式，一些较旧的应用程序可能会预计所有音频驱动程序都使用 WAVEFORMATEX 来指定这些格式。

如果驱动程序支持可明确指定为 WAVEFORMATEX 或 WAVEFORMATEXTENSIBLE 结构的音频格式，则驱动程序应识别该格式，而不管客户端应用程序或组件使用哪些结构来指定结构。 例如，如果音频设备支持 44.1 kHz 16 位立体声 PCM 格式，微型端口驱动程序的 KSPROPERTY\_PIN\_PROPOSEDATAFORMAT 属性处理程序，并且它的**newstream.ischecked**方法的实现应接受该格式不管格式是指定为 WAVEFORMATEX 还是 WAVEFORMATEXTENSIBLE 结构。

为了简化格式数据的处理，驱动程序通常使用 WAVEFORMATEXTENSIBLE 结构来表示格式。 此方法可能需要将输入 WAVEFORMATEX 结构转换为内部 WAVEFORMATEXTENSIBLE 表示形式，或将内部 WAVEFORMATEXTENSIBLE 表示形式转换为输出 WAVEFORMATEX 结构。

将格式描述符从 WAVEFORMATEX 转换为 WAVEFORMATEXTENSIBLE 时，如果 WAVEFORMATEX 结构的**wFormatTag**成员为波形\_格式\_PCM 或波形\_格式\_IEEE\_FLOAT，请将将 WAVEFORMATEXTENSIBLE 结构的成员 dwChannelMask 到 "扬声器\_前\_中心" （对于 mono 流）或 "扬声器"\_前面\_左侧 |扬声器\_正面\_右（适用于立体声流）。 在头文件 Ksmedia 中定义了扬声器\_前\_*XXX*常数。

在除 Windows 98 "黄金" 之外的所有 Windows 版本中，KMixer 支持一系列 WAVEFORMATEXTENSIBLE PCM 格式，这些格式具有多个通道，每个样本最多32位。

KMixer 支持的 WAVEFORMATEX PCM 格式的子集在 Windows 版本之间有所不同，如下表所示。

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
<th align="left">通道数量</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 98 "黄金"</p></td>
<td align="left"><p>8、16、24和32位</p></td>
<td align="left"><p>多渠道</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 98 SE</p></td>
<td align="left"><p>仅8和16位</p></td>
<td align="left"><p>仅单色和立体声</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 98 SE + 修补程序</p></td>
<td align="left"><p>8、16、24和32位</p></td>
<td align="left"><p>仅单色和立体声</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 2000</p></td>
<td align="left"><p>仅8和16位</p></td>
<td align="left"><p>仅单色和立体声</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Me</p></td>
<td align="left"><p>8、16、24和32位</p></td>
<td align="left"><p>仅单色和立体声</p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows XP 及更高版本</p></td>
<td align="left"><p>仅8和16位</p></td>
<td align="left"><p>仅单色和立体声</p></td>
</tr>
</tbody>
</table>

 
在 WAVEFORMATEXTENSIBLE 中， **dwBitsPerSample**是容器大小，而**wValidBitsPerSample**是每个样本的有效数据位数。 容器总是在内存中对齐，并且必须将容器大小指定为八位的倍数。

在定义 WAVEFORMATEXTENSIBLE 结构之前，供应商必须向 Microsoft 注册每个新的 wave 格式，以便可以将官方，16位格式标记分配给格式。 （格式标记包含在 WAVEFORMATEX 结构的**wFormatTag**成员中。）已注册的格式标记的列表显示在公共头文件 Mmreg 中（例如，波形\_格式\_MPEG）。

对于 WAVEFORMATEXTENSIBLE，不再需要注册格式。 供应商可以根据需要将 Guid 单独分配给其新格式。 （格式 GUID 包含在 WAVEFORMATEXTENSIBLE 的**SubFormat**成员中。）但是，Microsoft 在公共头文件 Ksmedia 中列出了一些更常用的格式 Guid （例如，KSDATAFORMAT\_子类型\_MPEG）。 在定义新格式 GUID 之前，供应商应检查 Ksmedia 中的 KSDATAFORMAT\_子 *\_类型*的列表，以确定是否已为特定格式定义了相应的 GUID。

使用 WAVEFORMATEXTENSIBLE 时，请将**wFormatTag**设置为波形\_格式\_可扩展，并**SubFormat**设置为合适的格式 GUID。 对于 "整数 PCM 格式"，请将**SubFormat**设置为 KSDATAFORMAT\_子类型\_PCM。 对于将示例值编码为浮点数的 PCM 格式，请将**SubFormat**设置为 KSDATAFORMAT\_子类型\_IEEE\_FLOAT。 对于这两种格式，请将**cbSize**设置为**sizeof**（WAVEFORMATEXTENSIBLE） **-sizeof**（WAVEFORMATEX）。 有关使用 WAVEFORMATEXTENSIBLE 描述非 PCM 数据格式的信息，请参阅[支持非 Pcm 波浪格式](supporting-non-pcm-wave-formats.md)。

 

 




