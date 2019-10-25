---
title: 针对动态子设备的驱动程序支持
description: 针对动态子设备的驱动程序支持
ms.assetid: ca355dfc-46ad-4df2-ac48-f3a0780dc3d3
keywords:
- 动态音频 subdevices WDK 音频
- 动态拓扑音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc7cfb682404a8e68cb461e26854f0c10ac07c04
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833810"
---
# <a name="driver-support-for-dynamic-subdevices"></a>针对动态子设备的驱动程序支持


[Subdevice 创建](subdevice-creation.md)中的代码示例演示如何使用**PcRegisterSubdevice**例程注册 Subdevice。 Windows 驱动程序工具包（WDK）中的 SB16 示例音频驱动程序演示了如何使用**PcRegisterPhysicalConnection**例程在同一音频适配器中的 subdevices 之间注册物理连接。

[IUnregisterSubdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregistersubdevice)和[IUnregisterPhysicalConnection](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregisterphysicalconnection)接口补充 PcRegister*Xxx*例程。 这些接口包含示例驱动程序用于 "取消注册" 设备的方法，这些方法是以前通过调用 PcRegister*Xxx*例程注册的。 如前所述，这两个接口在 Windows Server 2003 SP1 及更高版本和 Windows XP SP2 （而不是在早期版本的 Windows 版本）中提供。 因此，尽管 Windows Server 2003、Windows XP 和 Windows 2000 支持动态拓扑的热修复包，但早期版本的 Windows 版本不支持动态拓扑。

 

 




