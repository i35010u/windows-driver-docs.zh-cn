---
title: 简化驱动程序安装的函数
description: 简化驱动程序安装的函数
ms.assetid: 7201b260-6239-4c76-8d48-7e2df9c662cd
keywords:
- 功能 WDK，简化驱动程序安装
- DiInstallDevice
- DiInstallDriver
- DiRollbackDriver
- UpdateDriverForPlugAndPlayDevices
- PnP WDK 设备安装
- 即插即用 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c171b1adc508bde47dc8db76877e22b5c3aaeac
ms.sourcegitcommit: 34e36b185a28886752b0245f1b95858b75578e5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "74868209"
---
# <a name="functions-that-simplify-driver-installation"></a>简化驱动程序安装的函数


安装应用程序可以使用以下函数来简化 PnP 函数驱动程序的安装。

### <a href="" id="diinstalldevice--windows-vista-and-later-versions-of-windows-"></a>DiInstallDevice （Windows Vista 和更高版本的 Windows）

[**DiInstallDevice**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldevice)函数将安装特定驱动程序，该驱动程序安装在系统中的特定设备上的[驱动程序存储区](driver-store.md)中。

如果以下两个条件都成立，则安装应用程序应仅使用此函数：

-   应用程序合并了多个相同类型的设备实例，即所有设备实例都具有相同的硬件 Id 和兼容 Id。

-   应用程序要求在设备实例上安装特定于设备实例的驱动程序。

否则，安装应用程序应使用[**DiInstallDriver**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)或[**UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)来安装最匹配设备的驱动程序。

调用方还可以调用**DiInstallDevice**来执行以下操作：

-   搜索与设备最匹配的预安装驱动程序，如果找不到，则显示该设备的 "发现新硬件" 向导。

-   禁止调用 "完成-安装页" 和 "完成-安装操作"。

-   在特定设备上安装 null 驱动程序。

-   通知调用方是否需要重启系统才能完成安装。

### <a href="" id="diinstalldriver--windows-vista-and-later-versions-of-windows-"></a>DiInstallDriver （Windows Vista 和更高版本的 Windows）

[**DiInstallDriver**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)函数预安装[驱动程序存储区](driver-store.md)中的[驱动程序包](driver-packages.md)，然后在系统中出现的所有设备上安装驱动程序，该系统具有硬件 ID 或与驱动程序包匹配的兼容 ID。

调用**DiInstallDriver**或[**UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)是安装应用程序为设备安装新驱动程序的最简单方法。 **DiInstallDriver**和**UpdateDriverForPlugAndPlayDevices**执行相同的基本安装操作。 不过， **UpdateDriverForPlugAndPlayDevices**支持其他安装选项。

默认情况下，如果驱动程序比设备上当前安装的驱动程序更适合于设备，则**DiInstallDriver**仅在设备上安装驱动程序。 有关 Windows 如何选择设备驱动程序的信息，请参阅[Windows 如何选择驱动程序](how-setup-selects-drivers.md)。

调用方还可以调用**DiInstallDriver**来执行以下操作：

-   强制安装指定的驱动程序，而不管驱动程序是否比当前安装在设备上的驱动程序更适合于设备。

    **警告**   强制安装驱动程序可能会导致使用更兼容或更旧的驱动程序替换更兼容或更高的驱动程序。

     

-   向调用方指示是否需要重启系统才能完成安装。

### <a href="" id="dirollbackdriver--windows-vista-and-later-versions-of-windows-"></a>DiRollbackDriver （Windows Vista 和更高版本的 Windows）

[**DiRollbackDriver**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-dirollbackdriver)函数使用为设备设置的以前安装的备份驱动程序替换设备上当前安装的驱动程序。 如果设备在更新设备的驱动程序后失败，主要提供此功能以将设备还原到工作状态。 如果用户在设备管理器的设备的驱动程序页面上单击 "**回滚驱动程序**"，则此函数将执行相同的操作。

对于一个设备，Windows 最多维护一个备份驱动程序。 在设备上成功安装了驱动程序，并且 Windows 确定设备正常运行后，windows 会立即将驱动程序设置为设备的备份驱动程序。 但是，如果驱动程序未在设备上成功安装或在安装后设备无法正常工作，则 Windows 不会将驱动程序设置为设备的备份驱动程序。

调用方还可以调用**DiRollbackDriver**来执行以下操作：

-   禁止显示与驱动程序回滚关联的任何用户界面组件。

-   向调用方指示是否需要重启系统才能完成安装。

有关驱动程序回滚的详细信息，请参阅帮助和支持中心中设备管理器的相关信息。

### <a href="" id="updatedriverforplugandplaydevices"></a>UpdateDriverForPlugAndPlayDevices

[**UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)函数将驱动程序安装在系统中存在的硬件 id 或兼容 ID 与驱动程序包匹配的所有设备上。

调用此函数或[**DiInstallDriver**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)是安装应用程序安装新驱动程序的最简单方法，该驱动程序是系统中设备的最佳匹配项。 **UpdateDriverForPlugAndPlayDevices**的基本操作类似于**DiInstallDriver**的操作。 不过， **UpdateDriverForPlugAndPlayDevices**支持其他安装选项。

默认情况下，如果驱动程序比设备上当前安装的驱动程序更适合于设备，则**UpdateDriverForPlugAndPlayDevices**仅在设备上安装驱动程序。

调用方还可以选择调用**UpdateDriverForPlugAndPlayDevices**来执行以下操作：

-   强制安装指定的驱动程序，而不管驱动程序是否比当前安装在设备上的驱动程序更适合于设备。

    **警告**   强制安装驱动程序可能会导致使用更兼容或更旧的驱动程序替换更兼容或更高的驱动程序。

     

-   禁止复制、重命名或删除安装文件。

-   禁止显示用户界面组件。

-   向调用方指示是否需要重启系统才能完成安装。

 

 





