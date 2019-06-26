---
title: 音频流对象接口
description: 音频流对象接口
ms.assetid: 9d68016a-ddb1-4fbb-b6cc-384f8c76552c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e05d2cfaf56eab015e6ad9c3fc08a07db8e6b71e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355644"
---
# <a name="audio-stream-object-interfaces"></a>音频流对象接口


## <span id="ddk_audio_stream_object_interfaces_ks"></span><span id="DDK_AUDIO_STREAM_OBJECT_INTERFACES_KS"></span>


本部分介绍音频流对象接口。 这些接口是与批关联和 MIDI 流式传输到和从球瓶批，MIDI，该流和 DirectMusic 筛选器。 一些这些接口是由微型端口驱动程序实现，公开给端口驱动程序。 其他由端口驱动程序实现并公开给微型端口驱动程序。

本部分讨论以下音频流对象接口：

管理 DirectMusic 流的缓冲区存储。 由 Dmu 端口驱动程序实现。

将分配[数字版权管理 (DRM)](https://docs.microsoft.com/windows-hardware/drivers/audio/digital-rights-management)到音频流中的数字内容保护。 由 WaveCyclic、 WavePci 或 WaveRT 微型端口驱动程序实现。

表示通过 pin MIDI 筛选器上流动的 MIDI 流。 实现的 MIDI 微型端口驱动程序。

表示通过 pin WaveCyclic 筛选器上流动的批流。 由 WaveCyclic 微型端口驱动程序实现。

表示通过 pin WavePci 筛选器上流动的批流。 由 WavePci 微型端口驱动程序实现。

表示通过 pin WaveRT 筛选器上流动的批流。 WaveRT 微型端口 dirver 由实现。

扩充**IMiniportWaveRTStream**界面，提供对于 DMA 驱动程序的事件通知的其他方法。

表示通过 MIDI 或 DirectMusic pin DirectMusic 筛选器上流动的 MIDI 流。 由 Dmu 微型端口驱动程序实现。

提供映射服务添加到 WavePci 微型端口驱动程序的流对象。 由 WavePci 端口驱动程序实现。

处理 DirectMusic 合成器设备的 wave 输出。 由 Dmu 微型端口驱动程序实现并由 Dmu 端口驱动程序的批接收器。

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iallocatormxf)

[IDrmAudioStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nn-drmk-idrmaudiostream)

[IMiniportMidiStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidistream)

[IMiniportWaveCyclicStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavecyclicstream)

[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepcistream)

[IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavertstream)

[IMiniportWaveRTStreamNotofication](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavertstreamnotification)

[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imxf)

[IPortWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavepcistream)

[ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-isynthsinkdmus)

 

 





