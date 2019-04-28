---
title: MIDI 端口驱动程序
description: MIDI 端口驱动程序
ms.assetid: 4b403569-75c8-4cf4-bda1-efa9e004b529
keywords:
- MIDI 端口驱动程序 WDK 音频
- PortCls WDK 音频，端口驱动程序
- 音频的微型端口驱动程序 WDK，端口驱动程序
- 微型端口驱动程序 WDK 音频，端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f11d78e2ea06e7b6455fa52031819a47209dd326
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332317"
---
# <a name="midi-port-driver"></a>MIDI 端口驱动程序


## <span id="midi_port_driver"></span><span id="MIDI_PORT_DRIVER"></span>


MIDI 端口驱动程序管理 MIDI 合成器或捕获设备。 适配器驱动程序提供了相应[MIDI 微型端口驱动程序](midi-miniport-driver.md)绑定到 MIDI 端口驱动程序对象以形成 MIDI 筛选器 (请参阅[MIDI 和 DirectMusic 筛选器](midi-and-directmusic-filters.md))，可以捕获或呈现 MIDI流。

MIDI 端口驱动程序公开[IPortMidi](https://msdn.microsoft.com/library/windows/hardware/ff536891)微型端口驱动程序的接口。 **IPortMidi**继承基接口中的方法[IPort](https://msdn.microsoft.com/library/windows/hardware/ff536842)。 **IPortMidi**提供了以下其他方法：

[**IPortMidi::Notify**](https://msdn.microsoft.com/library/windows/hardware/ff536893)

通知的 MIDI 合成器或捕获设备具有高级到 MIDI 流中的新位置的端口驱动程序。
[**IPortMidi::RegisterServiceGroup**](https://msdn.microsoft.com/library/windows/hardware/ff536895)

注册端口驱动程序的服务组对象。
服务组包含一系列的微型端口驱动程序调用时要调用的一个或多个服务例程**通知**; 有关详细信息，请参阅[接收器服务和服务组对象](service-sink-and-service-group-objects.md)。

MIDI 端口和微型端口驱动程序对象与彼此通信通过其各自**IPortMidi**并[IMiniportMidi](https://msdn.microsoft.com/library/windows/hardware/ff536703)接口。 微型端口驱动程序将使用端口驱动程序**IPortMidi**接口以通知端口驱动程序的硬件中断。 此外，端口驱动程序与微型端口驱动程序的流对象通过其[IMiniportMidiStream](https://msdn.microsoft.com/library/windows/hardware/ff536704)接口。

在 Windows XP 及更高版本， **IPortMidi**并[IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)接口都实现在单个内部驱动程序的模块中。 这种整合得益于这两个接口的相似性。 例如，对于这两个接口定义的相同方法。 对于以前版本的 Windows，应看到的行为方面没有变化编写的应用程序**IPortMidi**并**IPortDMus**所得合并的 MIDI 和 Dmu 端口驱动程序的接口。

 

 




