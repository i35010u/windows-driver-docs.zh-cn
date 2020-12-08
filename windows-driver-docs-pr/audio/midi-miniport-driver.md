---
title: MIDI 微型端口驱动程序
description: MIDI 微型端口驱动程序
keywords:
- 音频微型端口驱动程序 WDK、MIDI
- 微型端口驱动程序 WDK 音频、MIDI
- MIDI 微型端口驱动程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42739cfb6420d2d09f7191531674b65d7a5de688
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801021"
---
# <a name="midi-miniport-driver"></a>MIDI 微型端口驱动程序


## <span id="midi_miniport_driver"></span><span id="MIDI_MINIPORT_DRIVER"></span>


MIDI 微型端口驱动程序管理简单 MIDI 设备的硬件相关功能，这些功能缺乏高级功能，如硬件顺序和可下载声音 (DL) 。 MIDI 端口驱动程序处理 MIDI 消息传递到合成程序的时间。 MIDI 微型端口驱动程序只负责向合成器传输 MIDI 消息，以响应来自端口驱动程序的请求。 具有高级 MIDI 功能的设备应改为使用 [dmu 微型端口驱动程序](dmus-miniport-driver.md) 。

MIDI 微型端口驱动程序应实现两个接口：

-   *微型端口接口* 初始化微型端口对象并创建 MIDI 流。

-   *流接口* 管理 MIDI 流并公开大多数微型端口驱动程序的功能。

微型端口接口 [IMiniportMidi](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)继承了 [IMiniport](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport) 接口中的方法。 **IMiniportMidi** 提供了以下附加方法：

[**IMiniportMidi：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-init)

初始化微型端口对象。

[**IMiniportMidi：： Newstream.ischecked**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-newstream)

创建新的流对象。

[**IMiniportMidi：： Service**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-service)

通知服务请求的微型端口驱动程序。

流接口 [IMiniportMidiStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidistream)继承 **IUnknown** 接口中的方法。 **IMiniportMidiStream** 提供了以下附加方法：

[**IMiniportMidiStream：： Read**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidistream-read)

从 MIDI 捕获设备读取输入数据。

[**IMiniportMidiStream::SetFormat**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidistream-setformat)

设置 MIDI 流的数据格式。

[**IMiniportMidiStream：： SetState**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidistream-setstate)

设置 MIDI 流的状态。

[**IMiniportMidiStream：： Write**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidistream-write)

将输出数据写入 MIDI 合成器。

MIDI 端口驱动程序可处理两个方向的所有计时问题，并依赖于微型端口驱动程序来响应端口驱动程序对 **IMiniportMidiStream** 读和写方法的调用，以便在适配器上快速移动数据。

PortCls 包含用于 MIDI 设备的内置 MIDI 微型端口驱动程序，这些设备具有调频合成和 UART 函数。 有关详细信息，请参阅 [**PcNewMiniport**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport)。

 

