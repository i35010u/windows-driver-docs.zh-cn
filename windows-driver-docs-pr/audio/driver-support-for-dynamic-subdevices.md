---
title: 针对动态子设备的驱动程序支持
description: 针对动态子设备的驱动程序支持
ms.assetid: ca355dfc-46ad-4df2-ac48-f3a0780dc3d3
keywords:
- 动态子音频设备 WDK 音频
- 动态拓扑 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d7d124b9c69afa3aad725848a607538616e3311
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360106"
---
# <a name="driver-support-for-dynamic-subdevices"></a>针对动态子设备的驱动程序支持


中的代码示例[子创建](subdevice-creation.md)演示如何使用**PcRegisterSubdevice**例程，以注册子。 SB16 示例音频驱动程序在 Windows Driver Kit (WDK) 演示如何使用**PcRegisterPhysicalConnection**例程，以注册相同的音频适配器中包含的子设备之间的物理连接。

[IUnregisterSubdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iunregistersubdevice)并[IUnregisterPhysicalConnection](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iunregisterphysicalconnection)接口补充 PcRegister*Xxx*例程。 这些接口包含示例驱动程序将使用"注销"之前通过调用 PcRegister 已注册的设备的方法*Xxx*例程。 正如前面提到的这两个接口是在 Windows Server 2003 SP1 和更高版本和 Windows XP sp2，但不是在早期 Windows 版本中可用。 因此，早期的 Windows 版本缺少对动态拓扑的支持，尽管使用动态拓扑支持的修补程序包是适用于 Windows Server 2003、 Windows XP 和 Windows 2000。

 

 




