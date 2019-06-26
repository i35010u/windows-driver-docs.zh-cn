---
title: 可简化驱动程序安装的 SetupAPI 函数
description: 可简化驱动程序安装的 SetupAPI 函数
ms.assetid: 7201b260-6239-4c76-8d48-7e2df9c662cd
keywords:
- 安装程序 Api 函数 WDK，从而简化了驱动程序安装
- DiInstallDevice
- DiInstallDriver
- DiRollbackDriver
- UpdateDriverForPlugAndPlayDevices
- 即插即用 WDK 设备安装，安装程序 Api
- 即插即用 WDK 设备安装，安装程序 Api
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fceae2a2f3771f4eda0aeeac23ebc4eb431ced52
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386400"
---
# <a name="setupapi-functions-that-simplify-driver-installation"></a>可简化驱动程序安装的 SetupAPI 函数


安装应用程序可以使用以下安装程序 Api 函数来简化安装的即插即用功能驱动程序。

### <a href="" id="diinstalldevice--windows-vista-and-later-versions-of-windows-"></a> DiInstallDevice （Windows Vista 和更高版本的 Windows）

[ **DiInstallDevice** ](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldevice)函数安装特定驱动程序中已预装[驱动程序存储区](driver-store.md)系统中的特定设备上。

如果以下条件都成立，安装应用程序应仅使用此函数：

-   应用程序包含多个相同类型的设备实例，也就是说，设备的所有实例都具有相同的硬件 Id 和兼容 Id。

-   应用程序需要特定于实例的设备的驱动程序，在设备实例上安装。

否则，安装应用程序应使用[ **DiInstallDriver** ](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)或[ **UpdateDriverForPlugAndPlayDevices** ](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)安装是与最匹配的设备驱动程序。

此外可以调用调用方**DiInstallDevice**来执行以下操作：

-   搜索与该设备，最佳匹配的预安装驱动程序，如果未找到，显示设备的发现新硬件向导。

-   取消调用完成安装页和完成安装操作。

-   在特定设备上安装的为 null 的驱动程序。

-   通知调用方是否需要重新启动系统才能完成安装。

### <a href="" id="diinstalldriver--windows-vista-and-later-versions-of-windows-"></a> DiInstallDriver （Windows Vista 和更高版本的 Windows）

[ **DiInstallDriver** ](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)函数预安装[驱动程序包](driver-packages.md)中[驱动程序存储区](driver-store.md)，然后在所有设备上安装该驱动程序该系统里有硬件的 ID 或兼容 ID 相匹配的驱动程序包。

调用**DiInstallDriver**或[ **UpdateDriverForPlugAndPlayDevices** ](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)是应用安装程序安装设备的新驱动程序的最简单方法。 **DiInstallDriver**并**UpdateDriverForPlugAndPlayDevices**执行相同的基本安装操作。 但是**UpdateDriverForPlugAndPlayDevices**支持更多安装选项。

默认情况下**DiInstallDriver**驱动程序是更好地匹配到设备项比当前安装在设备的驱动程序将仅在设备上安装驱动程序。 有关 Windows 如何选择设备的驱动程序的信息，请参阅[Windows 中如何选择驱动程序](how-setup-selects-drivers.md)。

此外可以调用调用方**DiInstallDriver**来执行以下操作：

-   强制不考虑该驱动程序是否比当前安装在设备的驱动程序到设备更好的匹配指定的驱动程序安装。

    **谨慎**  强制驱动程序的安装可能会导致更多兼容或更高版本的驱动程序替换为较低兼容或更低版本的驱动程序。

     

-   向调用方指示是否需要重新启动系统才能完成安装。

### <a href="" id="dirollbackdriver--windows-vista-and-later-versions-of-windows-"></a> DiRollbackDriver （Windows Vista 和更高版本的 Windows）

[ **DiRollbackDriver** ](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-dirollbackdriver)函数取代了以前安装的备份驱动程序，为设备设置的设备当前安装的驱动程序。 此函数主要用于设备还原为正常的工作环境，如果设备出现故障后更新设备驱动程序。 此函数执行相同操作，如果用户单击将执行**回滚驱动程序**设备在设备管理器的驱动程序页上。

Windows 维护最多一个备份设备驱动程序。 Windows 设置驱动程序，如设备驱动程序已成功在设备和 Windows 上安装之后立即备份驱动程序确定设备正常。 但是，如果驱动程序不会在设备上成功安装或设备无法正常工作在安装后，Windows 不将驱动程序设置作为设备的备份驱动程序。

此外可以调用调用方**DiRollbackDriver**来执行以下操作：

-   禁止显示驱动程序回滚与相关联的任何用户界面组件。

-   向调用方指示是否需要重新启动系统才能完成安装。

有关驱动程序回滚的详细信息，请参阅有关设备管理器中的帮助和支持中心中的信息。

### <a href="" id="updatedriverforplugandplaydevices"></a> UpdateDriverForPlugAndPlayDevices

[ **UpdateDriverForPlugAndPlayDevices** ](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)函数的所有设备上存在系统中有硬件 ID 或兼容 ID 相匹配的驱动程序包安装驱动程序。

调用此函数或[ **DiInstallDriver** ](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)是要安装新的驱动程序的设备的最佳匹配项是系统中安装应用程序的最简单方法。 基本操作**UpdateDriverForPlugAndPlayDevices**类似于的操作**DiInstallDriver**。 但是**UpdateDriverForPlugAndPlayDevices**支持更多安装选项。

默认情况下**UpdateDriverForPlugAndPlayDevices**驱动程序是更好地匹配到设备项比在设备当前安装的驱动程序将仅在设备上安装驱动程序。

可以选择性地调用调用方**UpdateDriverForPlugAndPlayDevices**来执行以下操作：

-   强制不考虑该驱动程序是否比当前安装在设备的驱动程序到设备更好的匹配指定的驱动程序安装。

    **谨慎**  强制驱动程序的安装可能会导致更多兼容或更高版本的驱动程序替换为较低兼容或更低版本的驱动程序。

     

-   禁止显示复制、 重命名或删除安装文件。

-   禁止显示用户界面组件。

-   向调用方指示是否需要重新启动系统才能完成安装。

 

 





