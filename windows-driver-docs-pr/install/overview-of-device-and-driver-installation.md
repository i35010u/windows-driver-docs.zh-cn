---
title: 设备和驱动程序安装概述
description: 设备和驱动程序安装概述
ms.assetid: 5f29635b-c41b-40d1-8b83-b7f5bc71413b
keywords:
- 设备安装程序 WDK 设备安装，有关设备安装
- 有关设备安装的设备安装 WDK，
- 安装设备 WDK，有关设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e5da2f5be09b5193c07a6f01a5b89689a165be8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575591"
---
# <a name="overview-of-device-and-driver-installation"></a>设备和驱动程序安装概述





Windows 提供了要安装的设备和驱动程序组件。 [系统提供的设备安装组件](system-provided-device-installation-components.md)适用于[供应商提供组件](vendor-provided-device-installation-components.md)安装设备。

Windows 安装设备时在系统重新启动和系统重新启动后的任何时候用户插入插 (PnP) 设备 （或手动安装非 PnP 设备） 时。 支持的即插即用，Windows 将继续基于在系统中，而不是用于结构化围绕驱动程序安装的设备的设备安装。 例如，而不是加载驱动程序的一组，并使这些驱动程序检测到它们支持的设备，Windows 确定系统和负载中存在的设备，并调用每个设备驱动程序。 驱动程序，如 ACPI 驱动程序和其他 PnP[总线驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540704)帮助 Windows 确定哪些设备是否存在。

## <a name="in-this-section"></a>本节内容


-   [如何将 Windows 安装的设备](how-windows-installs-devices.md)
-   [系统提供的设备安装组件](system-provided-device-installation-components.md)
-   [供应商提供的设备安装组件](vendor-provided-device-installation-components.md)
-   [设备安装文件](device-installation-files.md)
-   [设备安装类型](device-installation-types.md)
-   [Windows 中如何选择驱动程序](how-setup-selects-drivers.md)

有关设备管理和安装的详细信息，请参阅[驱动程序安装](https://go.microsoft.com/fwlink/p/?linkid=70230)网站。

 

 





