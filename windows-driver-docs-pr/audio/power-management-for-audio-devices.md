---
title: 音频设备的电源管理
description: 音频设备的电源管理
ms.assetid: 3d3d63af-5790-4760-9099-7116ed5a5446
keywords:
- 音频驱动程序 WDK、 电源管理
- 音频的微型端口驱动程序 WDK、 电源管理
- 微型端口驱动程序 WDK 音频，电源管理
- 电源管理 WDK 音频
- 端口类驱动程序 WDK 音频
- PortCls WDK 音频，电源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecd6228fa30e4a4de754d01d583a3af53eccc1eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328759"
---
# <a name="power-management-for-audio-devices"></a>音频设备的电源管理


## <span id="power_management_for_audio_devices"></span><span id="POWER_MANAGEMENT_FOR_AUDIO_DEVICES"></span>


PortCls 系统驱动程序将处理所有电源管理 Irp (请参阅[处理 Power Irp](https://msdn.microsoft.com/library/windows/hardware/ff546917)) 代表音频适配器驱动程序。 PortCls 通过适配器驱动程序通过调用来管理音频设备的电源状态[IAdapterPowerManagement](https://msdn.microsoft.com/library/windows/hardware/ff536485)并[IPowerNotify](https://msdn.microsoft.com/library/windows/hardware/ff536947)接口。 这两个接口是可选的。 可以更改其在响应来自 PortCls 的请求中的电源状态的设备适配器驱动程序可以公开 IAdapterPowerManagement 接口。 需要即将发生的电源关闭的提前警告的微型端口对象公开 IPowerNotify 接口。

在 Windows Server 2003 SP1，Windows XP SP2 和更高版本，PortCls 都使用计时器来确定何时要关闭音频段指定的超时时间内一直处于非活动状态的设备的电源。 超时发生时，PortCls 超时间隔和目标电源状态提供默认值。 硬件供应商可以选择重写这些默认值的特定于驱动程序的值。

本部分讨论以下主题：

[实现 IAdapterPowerManagement](implementing-iadapterpowermanagement.md)

[实现 IPowerNotify](implementing-ipowernotify.md)

[音频设备类的非活动计时器实现](audio-device-class-inactivity-timer-implementation.md)

 

 




