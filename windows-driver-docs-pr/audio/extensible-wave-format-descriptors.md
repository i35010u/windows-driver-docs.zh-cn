---
title: 可扩展的波形格式描述符
description: 可扩展的波形格式描述符
ms.assetid: b80e651b-fb97-4502-8526-e844425805dc
keywords:
- 波形格式描述符 WDK 音频
- 波浪格式说明符
- 波形格式标记 WDK 音频
- 波形流 WDK 音频
- 音频数据格式 WDK
- 数据格式化 WDK 音频，波形格式说明符
- 格式化 WDK 音频、波形格式说明符
- KSDATAFORMAT 结构
- WAVEFORMATEXTENSIBLE
- WAVEFORMATEX 结构
- WDM 音频数据格式 WDK
ms.date: 06/30/2020
ms.localizationpriority: medium
ms.openlocfilehash: a8abb89c09fd78287ce21fce145124ef468a9d4f
ms.sourcegitcommit: a260b60c121b25f06e8672afaaa8a3b197b17534
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85839123"
---
# <a name="extensible-wave-format-descriptors"></a>可扩展的波形格式描述符

下图显示了波形音频流的数据格式说明符。

![说明波形格式说明符的关系图](images/wavefmt.png)

如图所示，根据数据格式， [**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)结构后面的附加格式信息量会有所不同。

音频系统通过多种方式使用这种类型的格式描述符：

- 如上图中所示的格式描述符将作为调用参数传递给微型端口驱动程序的**newstream.ischecked**方法（例如，请参阅[**IMiniportWaveCyclic：： newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-newstream)）。

- [**IMiniport：:D atarangeintersection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection)方法的*ResultantFormat*参数指向一个缓冲区，此方法会将格式说明符写入其中，如上图中所示。

- [**KSPROPERTY \_ PIN \_ DATAINTERSECTION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataintersection)请求检索格式描述符，如上图中所示。

- [**KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-proposedataformat)请求接受格式描述符，如上图中所示。

- [**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)函数的*Connect*调用参数使用类似的格式。 此参数指向同时包含格式说明符的缓冲区开头的[**KSPIN \_ 连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect)结构。 紧跟在 KSPIN 连接结构后面的格式说明符以 \_ KSDATAFORMAT 结构开始，如上图中所示。

KSDATAFORMAT 结构后面的格式信息应为[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)结构。 WAVEFORMATEXTENSIBLE 是 WAVEFORMATEX 的扩展版本，可描述比 WAVEFORMATEX 更广泛的格式范围。

WAVEFORMAT 已过时，并且任何 Microsoft Windows 版本中的 WDM 音频子系统都不支持。 PCMWAVEFORMAT 结构是 WAVEFORMAT 的扩展版本，也已过时。

四个波形格式结构--WAVEFORMAT、PCMWAVEFORMAT、WAVEFORMATEX 和 WAVEFORMATEXTENSIBLE--都以从**wFormatTag**开始的相同的五个成员开头。 上图显示了这四个结构彼此重叠，以突出显示完全相同的结构部分。

WAVEFORMATEXTENSIBLE 通过添加三个成员，从 wValidBitsPerSample 开始扩展**WAVEFORMATEX。** （**示例**是使用其他成员**wValidSamplesPerBlock**，而不是**wValidBitsPerSample**来表示某些压缩格式的联合。）紧跟在缓冲区中 KSDATAFORMAT 结构末尾的**wFormatTag**成员指定 KSDATAFORMAT 后的格式信息类型。

与 WAVEFORMATEX 不同，WAVEFORMATEXTENSIBLE 可以执行以下操作：

1. 将每个样本的位数分别指定为样本容器的大小。 例如，可以在三个字节的容器内将一个20位的示例存储为左对齐。 WAVEFORMATEX 无法区分样本容器大小的每个样本的数据位数，无法明确地描述此类格式。

2. 将特定扬声器位置分配给多通道流中的音频通道。 WAVEFORMATEX 缺少此功能，只能支持单声道和（双通道）立体声流。

## <a name="legacy-use-of-waveformatex"></a>WAVEFORMATEX 的传统用法

WAVEFORMATEX 描述的任何格式也可以通过 WAVEFORMATEXTENSIBLE 说明。 有关将 WAVEFORMATEX 结构转换为 WAVEFORMATEXTENSIBLE 的信息，请参阅[在格式标记和 Subformat Guid 之间转换](converting-between-format-tags-and-subformat-guids.md)。

WAVEFORMATEX 足以描述大小为8或16位的示例格式，但必须使用 WAVEFORMATEXTENSIBLE 来充分描述样本精度大于16位的格式。 这里是两个示例：

- 采样精度为24位的流可以使用32位容器大小来有效处理，但可转换为使用24位容器来提高存储效率，而不会丢失数据。

- 处理包含24位样本数据的流时，仅提供20位精度的渲染设备可以使用仿色来改善其输出信号的保真度。 但是，仿色需要额外的处理时间，如果原始流精确到仅20位，则不需要进行额外的处理。

在这两个示例中，仅当样本精度和容器大小都已知时，才可以在处理和存储效率之间进行适当权衡时保留信号质量。

如果 WAVEFORMATEX 或 WAVEFORMATEXTENSIBLE 结构可以明确描述简单格式，则音频驱动程序可以选择使用任一结构来描述格式。 但是，音频驱动程序通常使用 WAVEFORMATEX 来指定带有8位或16位样本的 mono 和（双通道）立体声 PCM 格式，一些较旧的应用程序可能会预计所有音频驱动程序都使用 WAVEFORMATEX 来指定这些格式。

如果驱动程序支持可明确指定为 WAVEFORMATEX 或 WAVEFORMATEXTENSIBLE 结构的音频格式，则无论客户端应用程序或组件使用哪种结构来指定结构，驱动程序都应该识别格式。 例如，如果音频设备支持 44.1 kHz 16 位立体声 PCM 格式，微型端口驱动程序的 KSPROPERTY \_ 引脚 \_ PROPOSEDATAFORMAT 属性处理程序及其**newstream.ischecked**方法的实现应接受该格式，而不管格式是指定为 WAVEFORMATEX 还是 WAVEFORMATEXTENSIBLE 结构。

为了简化格式数据的处理，驱动程序通常使用 WAVEFORMATEXTENSIBLE 结构来表示格式。 此方法可能需要将输入 WAVEFORMATEX 结构转换为内部 WAVEFORMATEXTENSIBLE 表示形式，或将内部 WAVEFORMATEXTENSIBLE 表示形式转换为输出 WAVEFORMATEX 结构。

在 WAVEFORMATEXTENSIBLE 中， **dwBitsPerSample**是容器大小，而**wValidBitsPerSample**是每个样本的有效数据位数。 容器总是在内存中对齐，并且必须将容器大小指定为八位的倍数。
