---
title: 音频设备的电源管理
description: 音频设备的电源管理
ms.assetid: 3d3d63af-5790-4760-9099-7116ed5a5446
keywords:
- 音频驱动程序 WDK，电源管理
- 音频微型端口驱动程序 WDK，电源管理
- 微型端口驱动程序 WDK 音频，电源管理
- 电源管理 WDK 音频
- 端口类驱动程序 WDK 音频
- PortCls WDK 音频，电源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c98bd34b8ec6b927a4a15e6c8d0cac17c9d650f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210457"
---
# <a name="power-management-for-audio-devices"></a>音频设备的电源管理


## <span id="power_management_for_audio_devices"></span><span id="POWER_MANAGEMENT_FOR_AUDIO_DEVICES"></span>


PortCls 系统驱动程序处理所有电源管理 Irp (参阅代表音频适配器驱动程序 [处理电源 irp](../kernel/handling-power-irps.md)) 。 PortCls 通过适配器驱动程序的 [IAdapterPowerManagement](/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpowermanagement) 和 [IPowerNotify](/windows-hardware/drivers/ddi/portcls/nn-portcls-ipowernotify) 接口进行调用，来管理音频设备的电源状态。 这两个接口都是可选的。 对于可以更改其电源状态以响应来自 PortCls 的请求的设备，适配器驱动程序应公开 IAdapterPowerManagement 接口。 需要提前警告即将断电的微型端口对象应公开 IPowerNotify 接口。

在 Windows Server 2003 SP1、Windows XP SP2 及更高版本中，PortCls 使用计时器来确定何时关闭音频设备，这些设备在某些指定的超时时间间隔内处于非活动状态。 PortCls 为超时间隔提供默认值，并在出现超时时提供目标电源状态。 硬件供应商可以选择用其自己的特定于驱动程序的值覆盖这些默认值。

本部分介绍以下主题：

[实现 IAdapterPowerManagement](implementing-iadapterpowermanagement.md)

[实现 IPowerNotify](implementing-ipowernotify.md)

[音频设备类不活动计时器实现](audio-device-class-inactivity-timer-implementation.md)

 

