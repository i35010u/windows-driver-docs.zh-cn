---
title: 针对动态子设备的驱动程序支持
description: 针对动态子设备的驱动程序支持
keywords:
- 动态音频 subdevices WDK 音频
- 动态拓扑音频
ms.date: 12/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: df30468aeec279b45b6c69cb234eaada02a095bd
ms.sourcegitcommit: 7bdf85c72841fbc2093c315f900c69d2eef6e3e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/23/2020
ms.locfileid: "97757886"
---
# <a name="driver-support-for-dynamic-subdevices"></a>针对动态子设备的驱动程序支持

[Subdevice 创建](subdevice-creation.md)中的代码示例演示如何使用 **PcRegisterSubdevice** 例程注册 Subdevice。 [示例音频驱动](sample-audio-drivers.md)程序中讨论的 Sysvad 示例驱动程序演示了如何使用 **PcRegisterPhysicalConnection** 例程在同一音频适配器中的 subdevices 之间注册物理连接。

[IUnregisterSubdevice](/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregistersubdevice)和 [IUnregisterPhysicalConnection](/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregisterphysicalconnection)接口补充 PcRegister *Xxx* 例程。 这些接口包含示例驱动程序用于 "取消注册" 设备的方法，这些方法是以前通过调用 PcRegister *Xxx* 例程注册的。 如前所述，这两个接口在 Windows Server 2003 SP1 及更高版本和 Windows XP SP2 （而不是在早期版本的 Windows 版本）中提供。
