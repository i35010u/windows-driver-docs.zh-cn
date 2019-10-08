---
title: 设备和驱动程序安装概述
description: 设备和驱动程序安装概述
ms.assetid: 5f29635b-c41b-40d1-8b83-b7f5bc71413b
keywords:
- 设备安装程序 WDK 设备安装，关于设备安装
- 设备安装 WDK，关于设备安装
- 安装设备 WDK，关于设备安装
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: cd853d1644253043b01273b5533523785bec5d72
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007590"
---
# <a name="overview-of-device-and-driver-installation"></a>设备和驱动程序安装概述





Windows 提供了用于安装设备和驱动程序的组件。 [系统提供的设备安装组件](system-provided-device-installation-components.md)使用[供应商提供的组件](vendor-provided-device-installation-components.md)来安装设备。

当用户插入即插即用（PnP）设备（或手动安装非 PnP 设备）后，Windows 将在系统重新启动时和在系统重新启动之后的任何时间安装设备。 为支持 PnP，Windows 将继续安装基于系统中设备的设备，而不是围绕驱动程序构建安装。 例如，Windows 会确定系统中存在的设备，并为每个设备加载并调用驱动程序，而不是加载一组驱动程序并使这些驱动程序检测到它们支持的设备。 诸如 ACPI 驱动程序和其他 PnP[总线驱动](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)程序之类的驱动程序有助于 Windows 确定哪些设备存在。

## <a name="in-this-section"></a>本节内容


-   [Windows 如何安装设备](how-windows-installs-devices.md)
-   [系统提供的设备安装组件](system-provided-device-installation-components.md)
-   [供应商提供的设备安装组件](vendor-provided-device-installation-components.md)
-   [设备安装文件](device-installation-files.md)
-   [设备安装类型](device-installation-types.md)
-   [Windows 如何选择驱动程序](how-setup-selects-drivers.md)

有关设备管理和安装的详细信息，请参阅[驱动程序安装](https://go.microsoft.com/fwlink/p/?linkid=70230)网站。

 

 





