---
title: MIDI 端口驱动程序
description: MIDI 端口驱动程序
ms.assetid: 4b403569-75c8-4cf4-bda1-efa9e004b529
keywords:
- MIDI 端口驱动程序 WDK 音频
- PortCls WDK 音频，端口驱动程序
- 音频微型端口驱动程序 WDK，端口驱动程序
- 微型端口驱动程序 WDK 音频、端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a45e573ecadab1d8d7ad2d096046d272942eb64
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211403"
---
# <a name="midi-port-driver"></a>MIDI 端口驱动程序


## <span id="midi_port_driver"></span><span id="MIDI_PORT_DRIVER"></span>


MIDI 端口驱动程序管理 MIDI 合成器或捕获设备。 适配器驱动程序提供了一个相应的 [MIDI 微型端口驱动程序，该驱动程序](midi-miniport-driver.md) 绑定到 midi 端口驱动程序对象以形成 midi 筛选器 (查看可捕获或呈现 midi 流) 的 [Midi 和 DirectMusic 筛选器](midi-and-directmusic-filters.md) 。

MIDI 端口驱动程序向微型端口驱动程序公开 [IPortMidi](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportmidi) 接口。 **IPortMidi** 继承基接口 [IPort](/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)中的方法。 **IPortMidi** 提供了以下附加方法：

[**IPortMidi：： Notify**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportmidi-notify)

通知端口驱动程序： MIDI 合成器或捕获设备已前进到 MIDI 流中的新位置。
[**IPortMidi::RegisterServiceGroup**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportmidi-registerservicegroup)

使用端口驱动程序注册服务组对象。
服务组包含一个或多个在微型端口驱动程序调用 **Notify**时要调用的服务例程的列表;有关详细信息，请参阅 [服务接收器和服务组对象](service-sink-and-service-group-objects.md)。

MIDI 端口和微型端口驱动程序对象通过各自的 **IPortMidi** 和 [IMiniportMidi](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi) 接口相互通信。 微型端口驱动程序使用端口驱动程序的 **IPortMidi** 接口通知端口驱动程序的硬件中断。 此外，端口驱动程序通过其 [IMiniportMidiStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidistream) 接口与微型端口驱动程序的流对象通信。

在 Windows XP 和更高版本中， **IPortMidi** 和 [IPortDMus](/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus) 接口都是在单个内部驱动程序模块中实现的。 此合并可通过这两个接口的相似性来实现。 例如，为这两个接口定义了相同的方法。 对于为以前版本的 Windows 编写的应用程序，应在 **IPortMidi** 和 **IPortDMus** 接口的行为上不发生任何变化，因为这会导致 MIDI 和 dmu 端口驱动程序的合并。

 

