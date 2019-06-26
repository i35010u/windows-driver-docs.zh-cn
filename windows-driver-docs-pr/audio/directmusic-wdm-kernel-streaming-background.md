---
title: DirectMusic WDM 内核流式处理后台
description: DirectMusic WDM 内核流式处理后台
ms.assetid: 851fa156-590a-43fb-9c49-df528f0ea608
keywords:
- DirectMusic 内核模式 WDK 音频，WDM 内核流式处理
- 内核模式 synths WDK 音频，WDM 内核流式处理
- WDM 内核流 WDK 音频
- 内核流 WDK 音频
- 端口驱动程序 WDK 音频，合成器
- 硬件加速 WDK 音频
- 微型端口驱动程序 WDK 音频，内核模式硬件加速
- 合成器 WDK 音频，内核模式硬件加速
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b273e4d327abcb5b912591aa4bbbd5031106e5af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356525"
---
# <a name="directmusic-wdm-kernel-streaming-background"></a>DirectMusic WDM 内核流式处理后台


## <span id="directmusic_wdm_kernel_streaming_background"></span><span id="DIRECTMUSIC_WDM_KERNEL_STREAMING_BACKGROUND"></span>


本部分可能可用于驱动程序编写人员新手到 DirectMusic 和 WDM 流式处理内核，或想要的内核模式体系结构的简要概述。 有经验的 WDM 音频驱动程序编写人员可能想要跳到[合成器微型端口驱动程序概述](synthesizer-miniport-driver-overview.md)。 有关内核流式处理的更多常规介绍，请参阅[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming)。

从历史上看，没有两种类型的 Windows 驱动程序：

-   Windows 95 型 VxDs

-   对于基于 NT 的操作系统的驱动程序

Windows 98 / 我包含 ntkern.vxd，具有所有 NT 内核服务，并允许大多数 NT 驱动程序在 Windows 98 上运行 / me 一起提供。 WDM 驱动程序使用 NT 驱动程序环境的跨平台兼容性。 它们还实现电源管理和插。

流式处理体系结构的 WDM 内核必须源于 ActiveMovie （后来成为了 DirectShow），在其中使用的筛选器链概念进行流式处理媒体。 链中的每个筛选器可能是用户模式下筛选器，一种用户模式代码的内核模式筛选器，为代理提供服务或甚至一段已封送处理的硬件的用户模式代码 (请参阅[使用内核流式处理代理使用 AVStream模块](https://docs.microsoft.com/windows-hardware/drivers/stream/using-avstream-with-the-kernel-streaming-proxy-module))。 此体系结构已引入 Windows 2000 内核创建内核流式处理。

"固定"术语来自最初 Microsoft DirectAnimation 和 DirectShow。 Pin 现可用于与另一个连接一个筛选器的目标的内核流式处理术语。 例如，当有两个筛选器-使用"out"pin 的第一个和"in"pin--与第二个可以连接球瓶，以便第一个筛选器可以将流数据传递给第二个筛选器。 有关详细信息，请参阅[音频筛选器关系图](audio-filter-graphs.md)。

流式处理内核现在是 WDM 的一部分，由 WDM 音频。 使用 DirectMusic [WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)作为内核模式组件，将其信息向下传入的 I/O 请求数据包 (Irp) 形式的内核模式。 所有 DirectMusic 接口都仅限 WDM。

WDM 内核流式处理音频筛选器链通常系统提供，但也可以由 Isv 和 Ihv 提供。 [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)是一个组件，用于管理筛选器链。 它查找筛选器，并挂接在一起以构造筛选器关系图。 (SysAudio 本身不是关系图的成员。)

不需要的内核流式处理的专家来实现 Dmu 微型端口驱动程序。 Microsoft 提供了大量的常见代码供应商可以利用为了简化为 DirectMusic 的写入筛选器。 供应商可以编写其微型端口驱动程序，使系统提供 Dmu 端口驱动程序的一般功能的使用。 这种方法是类似于其他 Windows 驱动程序体系结构使用的类驱动程序/微型驱动程序模型 (比较，请参阅[WDM 音频术语](wdm-audio-terminology.md))。

WDM 音频具有名为 PortCls 的组件 (请参阅[端口类适配器驱动程序和 PortCls 系统驱动程序](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver))，这是多个类型的音频筛选器的类驱动程序。 这些音频筛选器处理 PCI 波形设备、 cyclical DMA 波形设备和 MIDI 设备。 而不是引用作为驱动程序和微型驱动程序的驱动程序组件作为筛选器和筛选器的最小或，我们称它们为端口和微型端口驱动程序。 PortCls 包含 MIDI 端口驱动程序，例如。

每个端口驱动程序，可以有不同种类的微型端口驱动程序执行特定于设备的操作。 例如，在 Windows 98 中，没有一个 MIDI 端口驱动程序，不同的微型端口驱动程序可以连接到它，例如 MPU 401 设备以及 FM 合成器设备。 端口驱动程序序列 MIDI 数据而不考虑它是否将到 FM 或 MPU 设备相同的方式。 微型端口驱动程序处理实际播放 MIDI 数据详细的信息。

排序器是在 MIDI 端口驱动程序本身，因为它保留加盖时间戳数据，直到到期，则通过适当的微型端口驱动程序中播放。 例如，MPU 401 微型端口驱动程序将批数据发送到设备通过外部合成器模块。 通过端口驱动程序的批接收器管理微型端口驱动程序的输出。

MIDI 说明会微型端口驱动程序存储和当批接收器，这是 MIDI 端口驱动程序的一部分，要求提供下一个音频数据块，微型端口驱动程序会将所需的波形数据呈现到指定的内存位置。 有关此过程的详细信息，请参阅[DirectMusic 微型端口驱动程序接口](directmusic-miniport-driver-interface.md)。

Microsoft 提供了所有 MPUs 标准的微型端口驱动程序的功能。 因为 MPU 规范定义的确切硬件应执行的操作以及其如何响应，Microsoft 提供的微型端口驱动程序来处理 MPUs PortCls 的一部分。 所有具有 MPUs 的声卡可以使用此相同的微型端口驱动程序。

PortCls 只能附加到 MIDI 端口驱动程序中的内置微型端口驱动程序，因此 DirectMusic 引入 Dmu 端口驱动程序将附加到 Dmu 微型端口驱动程序。 Dmu 端口驱动程序处理 DirectMusic MIDI 序列化和其他函数，并管理 MIDI、 批和可下载的声音 (DL) 数据。 示例 MPU 401 适配器驱动程序 Windows Driver Kit (WDK) 中使用 Dmu 端口驱动程序和一个内置 PortCls Dmu 微型端口驱动程序。

如果你只需 MPU 401 功能，请使用内置 mpu401.sys 微型端口驱动程序，它附带了 WDK。 只需将其绑定到 Dmu 端口驱动程序并设置 IRQ。 此驱动程序之前，引用由所标识的内置接口**IID\_IPortMidi** （MIDI 端口中的驱动程序 PortCls） 和**IID\_IMiniportDriverUart**（MPU 401 微型端口驱动程序的内置 PortCls） 类 Guid (请参阅[ **PcNewPort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewport)并[ **PcNewMiniport** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewminiport)). 现在，mpu401.sys 驱动程序引用**CLSID\_PortDMus**并**CLSID\_MiniportDriverDMusUART** Guid，因此它可以支持 DirectMusic。

当 Dmu 端口驱动程序收到 MIDI 数据时，它将数据路由到定序器，对每个说明根据其时间戳进行排序。 当注意已到期时，sequencer 会将其传递到微型端口驱动程序。 微型端口驱动程序实现可以指定距离提前它想要预提取这些说明。

当 Dmu 端口驱动程序收到属性请求包含 DLS 数据 (请参阅[ **KSPROPERTY\_合成\_DLS\_下载**](https://docs.microsoft.com/previous-versions/ff537396(v=vs.85)))，会将请求直接路由它微型端口驱动程序。 由于这些是只是可以播放的声音，没有必要涉及排序器或批接收器，则在下载时。

 

 




