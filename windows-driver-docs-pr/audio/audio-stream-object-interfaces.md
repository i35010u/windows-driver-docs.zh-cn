---
title: 音频流对象接口
description: 音频流对象接口
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d74ecaabdd1c443230901ddd54d0cf6b1ee50cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784959"
---
# <a name="audio-stream-object-interfaces"></a>音频流对象接口


## <span id="ddk_audio_stream_object_interfaces_ks"></span><span id="DDK_AUDIO_STREAM_OBJECT_INTERFACES_KS"></span>


本节介绍音频流对象接口。 这些接口与声波、MIDI 和 DirectMusic 筛选器的 pin 流入和流出的声波和 MIDI 流相关联。 其中一些接口由微型端口驱动程序实现并向端口驱动程序公开。 其他方法由端口驱动程序实现并公开给微型端口驱动程序。

本节讨论以下音频流对象接口：

管理 DirectMusic 流的缓冲区存储。 由 Dmu 端口驱动程序实现。

向音频流中的数字内容分配 [数字版权管理 (DRM) ](./digital-rights-management.md) 保护。 由 WaveCyclic、WavePci 或 WaveRT 微型端口驱动程序实现。

表示流过 MIDI 筛选器上的 pin 的 MIDI 流。 通过 MIDI 微型端口驱动程序实现。

表示在 WaveCyclic 筛选器上流过某个插针的波形流。 由 WaveCyclic 微型端口驱动程序实现。

表示在 WavePci 筛选器上流过某个插针的波形流。 由 WavePci 微型端口驱动程序实现。

表示在 WaveRT 筛选器上流过某个插针的波形流。 由 WaveRT 微型端口 dirver 实现。

补充 **IMiniportWaveRTStream** 接口，为 DMA 驱动程序事件通知提供其他方法。

表示在 DirectMusic 筛选器上通过 MIDI 或 DirectMusic 的 pin 流。 由 Dmu 微型端口驱动程序实现。

向 WavePci 微型端口驱动程序的流对象提供映射服务。 由 WavePci 端口驱动程序实现。

为 DirectMusic 合成器设备处理波形输出。 由 Dmu 微型端口驱动程序实现，由 Dmu 端口驱动程序的 wave 接收器使用。

[IAllocatorMXF](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)

[IDrmAudioStream](/windows-hardware/drivers/ddi/drmk/nn-drmk-idrmaudiostream)

[IMiniportMidiStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidistream)

[IMiniportWaveCyclicStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclicstream)

[IMiniportWavePciStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream)

[IMiniportWaveRTStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream)

[IMiniportWaveRTStreamNotofication](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstreamnotification)

[IMXF](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)

[IPortWavePciStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavepcistream)

[ISynthSinkDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-isynthsinkdmus)

 

