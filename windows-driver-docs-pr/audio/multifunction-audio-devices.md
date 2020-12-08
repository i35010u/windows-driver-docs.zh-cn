---
title: 多功能音频设备
description: 多功能音频设备
keywords:
- WDM 音频驱动程序 WDK、多功能设备
- 音频驱动程序 WDK，多功能设备
- 多功能音频设备 WDK
- subdevices WDK 音频
- 多功能音频设备 WDK，关于多功能音频设备
- 多个函数音频设备 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a747814737df3a0651d7c76a0c89e3cf80bee5f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800997"
---
# <a name="multifunction-audio-devices"></a>多功能音频设备


## <span id="multifunction_audio_devices"></span><span id="MULTIFUNCTION_AUDIO_DEVICES"></span>


多功能设备是单个适配器卡，它将两个或多个单独的函数（ (或 subdevices) 合并在一起。 多功能设备可以包含两个或更多音频 subdevices。 它还可能跨设备类。 例如，包含音频和调制解调器 subdevices 的设备属于媒体类和调制解调器类。 有关详细信息，请参阅 [支持多功能设备](../multifunction/index.md)。

PortCls 中的 WavePci 端口驱动程序对多功能设备施加特殊要求。 具体而言，适配器驱动程序必须提供一种方法来配置每个 subdevice，使其可以独立于多功能设备中的其他 subdevices 进行控制。 这可以通过以下两种方式之一为多功能设备设置 PCI 配置空间来实现：

1.  首选方法是为多功能设备上每个逻辑上不同的 subdevice 分配单独的设备 ID。 例如，如果你的多功能设备包含调制解调器、音频和操纵杆 subdevices，则系统应能够在 [设备树](../kernel/device-tree.md)中将每个 subdevice 都表示为独立的 devnode。 每个设备 ID 表示的 subdevice 具有其自己的 PCI 配置寄存器集，并与其他 subdevices 相互独立。 例如，启用或禁用 (音频 subdevice 的一个 subdevice （例如) 不会对调制解调器 (任何其他 subdevice 产生影响，例如) 。 这种类型的多功能设备不需要任何特定于硬件的驱动程序支持，而是 subdevices 本身的专有驱动程序。

2.  设计多功能设备的第二种方法是将单个设备 ID 作为一个整体分配给设备，并为单个 subdevices 提供单独的 PCI 基址寄存器 (条) 。 在此方案中，subdevices 共享一组通用的配置寄存器，但每个 subdevice 都有其自己的栏。 系统多功能驱动程序 (例如，在 Microsoft Windows 2000 和更高版本中 *Mf.sys* ;请参阅 [使用 System-Supplied 多功能总线驱动程序](../multifunction/using-the-system-supplied-multifunction-bus-driver.md)) 可以为每个 subdevice 的状态、命令和数据寄存器配置基址，而不影响其他函数的寄存器。 如果你的设备不是由 subdevice 在逻辑上分离的，则不能使用 PortCls 来管理你的设备。

本部分的其余部分介绍了实现前面列表中 (2) 的方法所需的步骤。 本文讨论了以下主题：

[多个音频子设备](multiple-audio-subdevices.md)

[多功能设备限制](multifunction-device-limits.md)

 

