---
title: WDM 音频驱动程序概述
description: Windows 驱动程序模型 (WDM) 音频驱动程序进行流式处理 (KS) 组件，它在内核模式下运行且属于操作系统内核的使用。
ms.assetid: 573a9b6d-6c50-40a6-9241-470ab418eb66
keywords:
- WDM 音频驱动程序 WDK
- 有关音频驱动程序的音频驱动程序 WDK，
- WDM 音频驱动程序 WDK，有关 WDM 音频驱动程序
- 供应商提供的驱动程序 WDK 音频
- 自定义的音频驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4475e8a39f2c999e3c534e05926cf40cbb5dcb72
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360026"
---
# <a name="wdm-audio-drivers-overview"></a>WDM 音频驱动程序概述


[Windows 驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)(WDM) 音频驱动程序使利用[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming)(KS) 组件，它在内核模式下运行且是操作系统的一部分。

硬件供应商应在开始开发基于 Windows 的音频硬件设备之前进行几项设计决策。

第一个决定是要设计需要一个供应商提供的自定义驱动程序将音频设备。 Windows 包含 PCI、 USB 和 IEEE 1394 符合 Microsoft 的设备的操作系统支持[通用音频体系结构](universal-audio-architecture.md)(UAA) 准则。 供应商不需要为 UAA 兼容音频设备提供自定义驱动程序。

但是，如果供应商提供自定义音频驱动程序是必需的供应商必须选择驱动程序是否应旨在与 PortCls 系统驱动程序 (Portcls.sys) 或 AVStream 类系统驱动程序 (Ks.sys) 配合工作。 PortCls 和 AVStream Windows 操作系统的一部分。 PortCls 是大多数音频适配器的正确选择。 有关 PortCls 详细信息，请参阅[简介端口类](introduction-to-port-class.md)。 有关 AVStream 详细信息，请参阅[AVStream 概述](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-overview)。

在设计时使用 PortCls 的自定义适配器驱动程序，可用于应用程序使用 WaveRT 进行音频适配器上的设备。 有关详细信息，请参阅[简介 WaveRT 端口驱动程序](introducing-the-wavert-port-driver.md)。

两个附加的决策涉及到如何显示拓扑和 pin 的数据范围指向音频的应用程序的适配器。 拓扑是逻辑数据路径和适配器电路中的控制节点的映射。 数据范围指定设备可以支持其批和 MIDI 流中的数据格式。 这两个决策会影响音频适配器上的设备对应用程序的显示方式。

在进行所有前面提到的决策时，硬件供应商必须权衡性能增强功能与成本实现它们的值。 另一个注意事项是特定的解决方案是否可以进行工作的 Windows 系列产品的数量。 本部分概述了这些问题以及对有关特定主题的更详细文档的引用。

本部分包括以下主题：

[通用音频体系结构](universal-audio-architecture.md)

[音频信号处理模式](audio-signal-processing-modes.md)

[自定义音频驱动程序](custom-audio-drivers.md)

[指定拓扑](specifying-the-topology.md)

[指定 Pin 数据范围](specifying-pin-data-ranges.md)

 

 




