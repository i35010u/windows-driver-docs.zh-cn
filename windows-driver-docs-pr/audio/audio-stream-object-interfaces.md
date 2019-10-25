---
title: 音频流对象接口
description: 音频流对象接口
ms.assetid: 9d68016a-ddb1-4fbb-b6cc-384f8c76552c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1507b4056738f299bf969fc72ff61f4a8d6e0eaa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831296"
---
# <a name="audio-stream-object-interfaces"></a>音频流对象接口


## <span id="ddk_audio_stream_object_interfaces_ks"></span><span id="DDK_AUDIO_STREAM_OBJECT_INTERFACES_KS"></span>


本节介绍音频流对象接口。 这些接口与声波、MIDI 和 DirectMusic 筛选器的 pin 流入和流出的声波和 MIDI 流相关联。 其中一些接口由微型端口驱动程序实现并向端口驱动程序公开。 其他方法由端口驱动程序实现并公开给微型端口驱动程序。

本节讨论以下音频流对象接口：

管理 DirectMusic 流的缓冲区存储。 由 Dmu 端口驱动程序实现。

将[数字版权管理（DRM）](https://docs.microsoft.com/windows-hardware/drivers/audio/digital-rights-management)保护分配给音频流中的数字内容。 由 WaveCyclic、WavePci 或 WaveRT 微型端口驱动程序实现。

表示流过 MIDI 筛选器上的 pin 的 MIDI 流。 通过 MIDI 微型端口驱动程序实现。

表示在 WaveCyclic 筛选器上流过某个插针的波形流。 由 WaveCyclic 微型端口驱动程序实现。

表示在 WavePci 筛选器上流过某个插针的波形流。 由 WavePci 微型端口驱动程序实现。

表示在 WaveRT 筛选器上流过某个插针的波形流。 由 WaveRT 微型端口 dirver 实现。

补充**IMiniportWaveRTStream**接口，为 DMA 驱动程序事件通知提供其他方法。

表示在 DirectMusic 筛选器上通过 MIDI 或 DirectMusic 的 pin 流。 由 Dmu 微型端口驱动程序实现。

向 WavePci 微型端口驱动程序的流对象提供映射服务。 由 WavePci 端口驱动程序实现。

为 DirectMusic 合成器设备处理波形输出。 由 Dmu 微型端口驱动程序实现，由 Dmu 端口驱动程序的 wave 接收器使用。

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)

[IDrmAudioStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nn-drmk-idrmaudiostream)

[IMiniportMidiStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidistream)

[IMiniportWaveCyclicStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclicstream)

[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream)

[IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream)

[IMiniportWaveRTStreamNotofication](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstreamnotification)

[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)

[IPortWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavepcistream)

[ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-isynthsinkdmus)

 

 





