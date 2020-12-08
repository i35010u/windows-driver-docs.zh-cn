---
title: DirectMusic WDM 内核流式处理后台
description: DirectMusic WDM 内核流式处理后台
keywords:
- DirectMusic 内核模式 WDK 音频，WDM 内核流式处理
- 内核模式 synths WDK 音频，WDM 内核流式处理
- WDM 内核流式处理 WDK 音频
- 内核流式处理 WDK 音频
- 端口驱动程序 WDK 音频，合成程序
- 硬件加速 WDK 音频
- 微型端口驱动程序 WDK 音频、内核模式硬件加速
- 合成 WDK 音频，内核模式硬件加速
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 101ae6d6807e4221617060de28d7a2d682f09aa8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789281"
---
# <a name="directmusic-wdm-kernel-streaming-background"></a>DirectMusic WDM 内核流式处理后台


## <span id="directmusic_wdm_kernel_streaming_background"></span><span id="DIRECTMUSIC_WDM_KERNEL_STREAMING_BACKGROUND"></span>


本部分对于不熟悉 DirectMusic 和 WDM 内核流式处理的驱动程序编写器或需要内核模式体系结构的简要概述的用户可能很有用。 经验丰富的 WDM 音频驱动程序编写器可能想跳过 [合成微型端口驱动程序概述](synthesizer-miniport-driver-overview.md)。 若要深入了解内核流式处理，请参阅 [内核流式处理](../stream/kernel-streaming.md)。

从历史上看，Windows 的驱动程序有两种类型：

-   Windows 95 样式 Vxd

-   基于 NT 的操作系统的驱动程序

Windows 98/Me 包含 ntkern，其中包含所有 NT 内核服务并允许大多数 NT 驱动程序在 Windows 98/Me 上运行。 WDM 驱动程序使用 NT 驱动程序环境实现跨平台兼容性。 它们还实现了电源管理和即插即用。

WDM 内核流式处理体系结构在 ActiveMovie 中具有其根 (这会成为 DirectShow) ，其中筛选器链的概念用于流式处理媒体。 链中的每个筛选器都可以是用户模式筛选器、一段作为内核模式筛选器的代理的用户模式代码，甚至是封送处理一段硬件的用户模式代码 (参阅将 [AVStream 与内核流式处理代理模块一起使用](../stream/using-avstream-with-the-kernel-streaming-proxy-module.md)) 。 此体系结构已进入 Windows 2000 内核，以创建内核流式处理。

"Pin" 术语最初来自 Microsoft DirectAnimation 和 DirectShow。 Pin 现在是目标的内核流式处理术语，可用于将一个筛选器与另一个筛选器进行连接。 例如，当有两个筛选器时，第一个具有 "out" pin，第二个筛选器具有 "in" pin--可以连接 pin，以便第一个筛选器可以将数据流传递到第二个筛选器。 有关详细信息，请参阅 [音频筛选器图](audio-filter-graphs.md)。

内核流现在是 WDM 的一部分，由 WDM 音频使用。 DirectMusic 使用 [WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver) 作为内核模式组件，并以 i/o 请求数据包的形式向下传递 (irp) 的内核模式。 所有 DirectMusic 接口都是严格的 WDM。

WDM 内核流音频筛选器链通常是系统提供的，但也可由 Isv 和 Ihv 提供。 [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)是管理筛选器链的组件。 它将查找筛选器并将它们挂钩在一起以构造筛选器关系图。  (SysAudio 不是图形的成员。 ) 

无需成为内核流式处理专家即可实现 Dmu 微型端口驱动程序。 Microsoft 提供了一组很大的常见代码，供应商可以利用它们来更轻松地编写 DirectMusic 的筛选器。 供应商可以编写其微型端口驱动程序，使用系统提供的 Dmu 端口驱动程序的一般功能。 此方法类似于其他 Windows 驱动程序体系结构 (使用的类 driver/微型驱动程序模型进行比较，请参阅 [WDM 音频术语](wdm-audio-terminology.md)) 。

WDM 音频包含一个名为 PortCls 的组件 (参阅 [端口类适配器驱动程序和 PortCls 系统驱动程序](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver)) ，这是多种类型的音频筛选器的类驱动程序。 这些音频过滤器处理 PCI wave 设备、循环 DMA wave 设备和 MIDI 设备。 我们将它们称为端口和微型端口驱动程序，而不是将驱动程序组件称为筛选器和小型筛选器或驱动程序和微型驱动程序。 例如，PortCls 包含 MIDI 端口驱动程序。

对于每个端口驱动程序，可以有不同类型的可执行设备特定操作的微型端口驱动程序。 例如，在 Windows 98 中，有一个 MIDI 端口驱动程序和不同的微型端口驱动程序可以连接到它，例如 MPU-401 设备和 FM 合成器设备。 端口驱动程序以相同的方式序列 MIDI 数据，无论它是转向 FM 还是 MPU 设备。 微型端口驱动程序处理实际播放 MIDI 数据的细节。

由于 sequencer 处于 MIDI 端口驱动程序本身，因此它将保留时间戳的数据直到它到期，然后通过适当的微型端口驱动程序播放它。 例如，MPU-401 微型端口驱动程序通过外部合成器模块将 wave 数据发送到设备。 微型端口驱动程序的输出由端口驱动程序的波形接收器进行管理。

微型端口驱动程序存储 MIDI 说明，当作为 MIDI 端口驱动程序的一部分的 wave 接收器要求下一个音频数据块时，微型端口驱动程序会将请求的波形数据呈现到指定的内存位置。 有关此过程的详细信息，请参阅 [DirectMusic 微型端口驱动程序接口](directmusic-miniport-driver-interface.md)。

Microsoft 为所有 MPUs 提供标准微型端口驱动程序功能。 由于 MPU 规范确切地定义了硬件应执行的操作及其响应方式，因此 Microsoft 提供了一个微型端口驱动程序来处理 MPUs 作为 PortCls 的一部分。 具有 MPUs 的所有声卡都可以使用此相同的微型端口驱动程序。

PortCls 中的内置微型端口驱动程序仅连接到 MIDI 端口驱动程序，因此 DirectMusic 引入了 Dmu 端口驱动程序以附加到 Dmu 微型端口驱动程序。 Dmu 端口驱动程序处理 MIDI 序列和 DirectMusic 的其他功能，并 (DL) 数据中管理 MIDI、波形和可下载声音。 Windows 驱动程序工具包中的 MPU-401 适配器驱动程序 (WDK) 使用 Dmu 端口驱动程序以及内置于 PortCls 的 Dmu 微型端口驱动程序之一。

如果你只需要 MPU-401 功能，请使用 WDK 随附的内置 mpu401.sys 微型端口驱动程序。 只需将其绑定到 Dmu 端口驱动程序并设置 IRQ 即可。 以前，此驱动程序引用了由 **IID \_ IPortMidi** 标识的内置接口，这些接口由 PortCls) 中的 MIDI 端口驱动程序和 **iid \_ IMiniportDriverUart** (内置于 PortCls) 类 guid 的 MPU-401 微型端口驱动程序 (参阅 [**PcNewPort**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport) 和 [**PcNewMiniport**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport))  (。 现在，mpu401.sys 驱动程序引用 **clsid \_ PortDMus** 和 **clsid \_ MiniportDriverDMusUART** Guid，以便它能够支持 DirectMusic。

当 Dmu 端口驱动程序接收 MIDI 数据时，它会将数据路由到 sequencer，这将基于其时间戳对每个注释进行排序。 当注释到期时，sequencer 会将其向下传递到微型端口驱动程序。 微型端口驱动程序实现可以指定预先提取这些说明的时间。

当 Dmu 端口驱动程序收到包含 DLS 数据的属性请求时 (参阅 [**KSPROPERTY \_ 合成 \_ dl) \_ 下载**](/previous-versions/ff537396(v=vs.85)) ，它会直接将请求路由到微型端口驱动程序。 由于这些只是可以播放的声音，因此在下载时无需涉及 sequencer 或波形接收器。

 

