---
title: MIDI 微型端口驱动程序
description: MIDI 微型端口驱动程序
ms.assetid: 38aeba40-35da-4bfd-a8fe-cf8f7e96f286
keywords:
- 音频的微型端口驱动程序 WDK MIDI
- 微型端口驱动程序 WDK 音频 MIDI
- MIDI 微型端口驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a018ddb93f1af9cd817067d2bc924bf8b3fec3f3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363240"
---
# <a name="midi-miniport-driver"></a>MIDI 微型端口驱动程序


## <span id="midi_miniport_driver"></span><span id="MIDI_MINIPORT_DRIVER"></span>


MIDI 微型端口驱动程序管理的简单 MIDI 设备缺少高级的功能，如硬件序列化和可下载的声音 (DL) 的硬件相关的函数。 MIDI 端口驱动程序处理向合成器传递 MIDI 消息的时间。 MIDI 微型端口驱动程序将仅负责将 MIDI 消息传输给请求响应端口驱动程序从合成器。 应使用具有高级 MIDI 功能的设备[Dmu 微型端口驱动程序](dmus-miniport-driver.md)相反。

MIDI 微型端口驱动程序应实现两个接口：

-   *微型端口接口*初始化微型端口对象并创建 MIDI 流。

-   *流接口*管理 MIDI 流，并会公开大部分的微型端口驱动程序的功能。

微型端口接口[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidi)，继承中的方法[IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiport)接口。 **IMiniportMidi**提供了以下其他方法：

[**IMiniportMidi::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidi-init)

初始化微型端口对象。

[**IMiniportMidi::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidi-newstream)

创建新的流对象。

[**IMiniportMidi::Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidi-service)

通知服务的请求的微型端口驱动程序。

流接口[IMiniportMidiStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidistream)，继承中的方法**IUnknown**接口。 **IMiniportMidiStream**提供了以下其他方法：

[**IMiniportMidiStream::Read**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidistream-read)

读取输入 MIDI 捕获设备中的数据。

[**IMiniportMidiStream::SetFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidistream-setformat)

设置 MIDI 流的数据格式。

[**IMiniportMidiStream::SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidistream-setstate)

设置 MIDI 流的状态。

[**IMiniportMidiStream::Write**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidistream-write)

将输出数据写入到 MIDI 合成器。

MIDI 端口驱动程序处理两个方向中的所有计时问题，并依赖于立即将数据移动和关闭响应到端口驱动程序的调用中的适配器的微型端口驱动程序**IMiniportMidiStream** read 和 write 方法。

PortCls 包含具有 FM 合成和 UART 函数的 MIDI 设备的内置 MIDI 微型端口驱动程序。 有关详细信息，请参阅[ **PcNewMiniport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewminiport)。

 

 




