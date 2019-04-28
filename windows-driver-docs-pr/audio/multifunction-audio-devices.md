---
title: 多功能音频设备
description: 多功能音频设备
ms.assetid: 6ef54b12-d0ea-4e55-afee-61f834375b92
keywords:
- WDM 音频驱动程序 WDK，多功能设备
- 音频驱动程序 WDK，多功能设备
- 多功能音频设备 WDK
- 子设备 WDK 音频
- 多功能音频设备 WDK，关于多功能音频设备
- 多个函数音频设备 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e62ece95af8c3122dc583b6c0437e1fb720ccfbe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332308"
---
# <a name="multifunction-audio-devices"></a>多功能音频设备


## <span id="multifunction_audio_devices"></span><span id="MULTIFUNCTION_AUDIO_DEVICES"></span>


多功能设备是单个适配卡，其中包含两个或多个单独的函数 （或子设备）。 多功能设备可以包含两个或多个音频子设备。 它可能会将设备类 s p a n。 包含音频和调制解调器子设备的设备，属于介质类和调制解调器类。 有关详细信息，请参阅[支持多功能设备](https://msdn.microsoft.com/library/windows/hardware/ff542743)。

中 PortCls 的 WavePci 端口驱动程序将置于多功能设备的特殊要求。 具体而言，适配器驱动程序必须提供一种方法来配置每个子，以便它可以独立于多功能设备中的其他子设备控制。 这可以通过设置多功能设备上的两种方式之一中的 PCI 配置空间完成：

1.  首选的方法是将单独的设备 ID 分配给每个逻辑独立子多功能设备上。 如果你的多功能设备包含调制解调器、 音频和游戏杆子设备，例如，系统应该能够表示为独立 devnode 中的每个子[设备树](https://msdn.microsoft.com/library/windows/hardware/ff543194)。 每个设备 ID 表示子有其自己的 PCI 配置寄存器集，并且与正交和独立于其他子设备。 例如，启用或禁用一个子 （音频子，例如） 应具有对任何其他子 （例如调制解调器） 没有影响。 多功能设备的此类型要求除了专有驱动程序没有特殊的特定于硬件的驱动程序支持的子设备本身。

2.  设计多功能设备第二种方法是将单个设备 ID 分配给作为一个整体设备并提供单独的 PCI 基址为各个子设备注册 （条形图）。 在此方案中，子设备共享一组通用的配置注册表，但每个子都有其自己条或图条。 系统多功能驱动程序 (例如， *Mf.sys* Microsoft Windows 2000 及更高版本; 请参阅[使用 System-Supplied 多功能总线驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff542778)) 可以为每个配置的基址独立于其他函数的寄存器子的状态、 命令和数据寄存器。 如果你的设备的条不是可由子逻辑上分离的则无法使用 PortCls 来管理你的设备。

本部分的剩余部分将介绍实现上述列表中的方法 (2) 所需的步骤。 论述了以下主题：

[多个音频子设备](multiple-audio-subdevices.md)

[多功能设备限制](multifunction-device-limits.md)

 

 




