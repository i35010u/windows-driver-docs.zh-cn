---
title: 电源管理和即插即用中视频微型端口驱动程序 (XDDM)
description: 视频微型端口驱动程序中的电源管理和即插即用（Windows 2000 模型）
ms.assetid: e5b2ac53-e492-43de-91a3-5b02c26ee9a3
keywords:
- 微型端口驱动程序 WDK Windows 2000，插
- 微型端口驱动程序 WDK Windows 2000 中，电源管理
- 即插即用 WDK 微型端口
- 即插即用 WDK 视频微型端口
- 电源管理 WDK 微型端口
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 189c3fcf5f2fafb70244bd73bc0ffe3f1c86f9e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352275"
---
# <a name="power-management-and-plug-and-play-in-video-miniport-drivers-windows-2000-model"></a>视频微型端口驱动程序中的电源管理和即插即用（Windows 2000 模型）


## <span id="ddk_plug_and_play_and_power_management_in_video_miniport_drivers_windo"></span><span id="DDK_PLUG_AND_PLAY_AND_POWER_MANAGEMENT_IN_VIDEO_MINIPORT_DRIVERS_WINDO"></span>


所有 Windows 2000 和更高版本的微型端口驱动程序必须都支持插和电源管理。 这包括如枚举子设备的能力*DDC*监视器、 内部集成电路 (I²C) 设备和辅助的适配器。

视频端口驱动程序管理的微型端口驱动程序，包括创建 FDO （功能的设备对象） 并接收和调度 PnP 特定 IRP 代码的即插即用要求的大多数 (请参阅[IRP 主要函数代码](https://msdn.microsoft.com/library/windows/hardware/ff550710)) 上微型端口驱动程序的代表。

微型端口驱动程序必须实现以下函数来支持即插即用和电源管理：

[*HwVidSetPowerState*](https://msdn.microsoft.com/library/windows/hardware/ff567365)

[*HwVidGetPowerState*](https://msdn.microsoft.com/library/windows/hardware/ff567336)

[*HwVidGetVideoChildDescriptor*](https://msdn.microsoft.com/library/windows/hardware/ff567341)

无法从系统中删除旧的微型端口驱动程序的图形适配器，而系统正在运行，也不会自动添加到正在运行的系统时检测到旧的微型端口驱动程序。

请参阅[的显示适配器 （Windows 2000 模式） 的子设备](child-devices-of-the-display-adapter--windows-2000-model-.md)有关检测和与适配器的子设备通信的详细信息。 有关插驱动程序的常规信息，请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)。

 

 





