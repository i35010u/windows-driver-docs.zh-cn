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
ms.openlocfilehash: 2b0ffa0ef538ca8e018427cfc2dd9125dc934cb6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363243"
---
# <a name="midi-port-driver"></a>MIDI 端口驱动程序


## <span id="midi_port_driver"></span><span id="MIDI_PORT_DRIVER"></span>


MIDI 端口驱动程序管理 MIDI 合成器或捕获设备。 适配器驱动程序提供了相应[MIDI 微型端口驱动程序](midi-miniport-driver.md)绑定到 MIDI 端口驱动程序对象以形成 MIDI 筛选器 (请参阅[MIDI 和 DirectMusic 筛选器](midi-and-directmusic-filters.md))，可以捕获或呈现 MIDI流。

MIDI 端口驱动程序公开[IPortMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportmidi)微型端口驱动程序的接口。 **IPortMidi**继承基接口中的方法[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iport)。 **IPortMidi**提供了以下其他方法：

[**IPortMidi::Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportmidi-notify)

通知的 MIDI 合成器或捕获设备具有高级到 MIDI 流中的新位置的端口驱动程序。
[**IPortMidi::RegisterServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportmidi-registerservicegroup)

注册端口驱动程序的服务组对象。
服务组包含一系列的微型端口驱动程序调用时要调用的一个或多个服务例程**通知**; 有关详细信息，请参阅[接收器服务和服务组对象](service-sink-and-service-group-objects.md)。

MIDI 端口和微型端口驱动程序对象与彼此通信通过其各自**IPortMidi**并[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidi)接口。 微型端口驱动程序将使用端口驱动程序**IPortMidi**接口以通知端口驱动程序的硬件中断。 此外，端口驱动程序与微型端口驱动程序的流对象通过其[IMiniportMidiStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidistream)接口。

在 Windows XP 及更高版本， **IPortMidi**并[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iportdmus)接口都实现在单个内部驱动程序的模块中。 这种整合得益于这两个接口的相似性。 例如，对于这两个接口定义的相同方法。 对于以前版本的 Windows，应看到的行为方面没有变化编写的应用程序**IPortMidi**并**IPortDMus**所得合并的 MIDI 和 Dmu 端口驱动程序的接口。

 

 




