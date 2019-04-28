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
ms.openlocfilehash: 8fb8fc53526cdfa404ae409321301ee2fde5b0bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332326"
---
# <a name="midi-miniport-driver"></a>MIDI 微型端口驱动程序


## <span id="midi_miniport_driver"></span><span id="MIDI_MINIPORT_DRIVER"></span>


MIDI 微型端口驱动程序管理的简单 MIDI 设备缺少高级的功能，如硬件序列化和可下载的声音 (DL) 的硬件相关的函数。 MIDI 端口驱动程序处理向合成器传递 MIDI 消息的时间。 MIDI 微型端口驱动程序将仅负责将 MIDI 消息传输给请求响应端口驱动程序从合成器。 应使用具有高级 MIDI 功能的设备[Dmu 微型端口驱动程序](dmus-miniport-driver.md)相反。

MIDI 微型端口驱动程序应实现两个接口：

-   *微型端口接口*初始化微型端口对象并创建 MIDI 流。

-   *流接口*管理 MIDI 流，并会公开大部分的微型端口驱动程序的功能。

微型端口接口[IMiniportMidi](https://msdn.microsoft.com/library/windows/hardware/ff536703)，继承中的方法[IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)接口。 **IMiniportMidi**提供了以下其他方法：

[**IMiniportMidi::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536709)

初始化微型端口对象。

[**IMiniportMidi::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536710)

创建新的流对象。

[**IMiniportMidi::Service**](https://msdn.microsoft.com/library/windows/hardware/ff536711)

通知服务的请求的微型端口驱动程序。

流接口[IMiniportMidiStream](https://msdn.microsoft.com/library/windows/hardware/ff536704)，继承中的方法**IUnknown**接口。 **IMiniportMidiStream**提供了以下其他方法：

[**IMiniportMidiStream::Read**](https://msdn.microsoft.com/library/windows/hardware/ff536705)

读取输入 MIDI 捕获设备中的数据。

[**IMiniportMidiStream::SetFormat**](https://msdn.microsoft.com/library/windows/hardware/ff536706)

设置 MIDI 流的数据格式。

[**IMiniportMidiStream::SetState**](https://msdn.microsoft.com/library/windows/hardware/ff536707)

设置 MIDI 流的状态。

[**IMiniportMidiStream::Write**](https://msdn.microsoft.com/library/windows/hardware/ff536708)

将输出数据写入到 MIDI 合成器。

MIDI 端口驱动程序处理两个方向中的所有计时问题，并依赖于立即将数据移动和关闭响应到端口驱动程序的调用中的适配器的微型端口驱动程序**IMiniportMidiStream** read 和 write 方法。

PortCls 包含具有 FM 合成和 UART 函数的 MIDI 设备的内置 MIDI 微型端口驱动程序。 有关详细信息，请参阅[ **PcNewMiniport**](https://msdn.microsoft.com/library/windows/hardware/ff537714)。

 

 




