---
title: 辅助安装程序操作
description: 辅助安装程序操作
ms.assetid: a7f52125-b435-4963-85dc-712700ba9fe9
keywords:
- 共同安装程序 WDK 设备安装，其工作原理
- 共同安装程序 WDK 设备安装示例
- SetupDiCallClassInstaller
- 类共同安装程序 WDK
- DIF 请求共同安装程序示例 WDK
- 特定于设备的共同安装程序 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f36cc41ac0c8b30ab0b28e85434b1457a06c7c06
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375329"
---
# <a name="co-installer-operation"></a>辅助安装程序操作





下图中所示，安装程序 Api，会调用共同安装程序。

![说明如何共同安装程序参与设备安装的关系图](images/coinsts.png)

无阴影的框表示操作系统提供的组件[系统提供的设备安装程序类](https://docs.microsoft.com/previous-versions/ff553419(v=vs.85))。 带阴影的框表示你可以提供的组件。 如果创建自定义设备安装程序类，还可以提供类安装程序。 但是，很少需要创建新的设备安装程序类，因为几乎每个设备可以是与一个系统提供的设备安装程序类相关联。 有关 Windows 组件的详细信息，请参阅[设备安装概述](overview-of-device-and-driver-installation.md)。

可以为特定设备提供共同安装程序 (*特定于设备的共同安装程序*) 或设备安装程序类 (*类共同安装程序*)。 仅在安装辅助安装程序为其注册的设备时，安装程序 Api 调用的特定于设备的共同安装程序。 操作系统和供应商可以注册零个或多个特定于设备的共同安装程序的设备。 安装程序 Api 调用类共同安装程序安装为其注册共同安装程序的设备安装程序任何的类设备时。 操作系统和供应商可以注册一个或多个类共同安装程序的设备安装程序类。 此外，可以为一个或多个安装程序类注册类共同安装程序。

Windows 和[自定义设备安装应用程序](writing-a-device-installation-application.md)安装的设备通过调用[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)与[设备安装函数代码](https://docs.microsoft.com/previous-versions/ff541307(v=vs.85))（DIF 代码）。

GUI 模式在安装期间，操作系统将调用[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller) DIF 代码以检测系统中存在的非 PnP 设备。 IHV 通常会提供的非 PnP 设备的 IHV 释放执行此操作的共同安装程序。

对于每个差异请求， **SetupDiCallClassInstaller**调用任何类共同安装程序已注册设备的安装程序类，为特定的设备，注册任何设备共同安装程序和提供的类安装程序设备的安装程序类，如果有一个系统。

自定义设备安装应用程序必须调用**SetupDiCallClassInstaller**而不是直接调用共同安装程序或类的安装程序。 此函数可确保相应地调用所有已注册的共同安装程序。

设备在安装之前，通常注册类共同安装程序和特定于设备的共同安装程序均将注册为设备的安装的一部分。 类共同安装程序会因此通常添加到共同安装程序列表在首次生成时，在设备安装过程中调用的所有差异请求。

操作系统将特定于设备的共同安装程序添加到共同安装程序列表后[ **DIF_REGISTER_COINSTALLERS** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-register-coinstallers)请求已完成的设备 (或[ **SetupDiRegisterCoDeviceInstallers** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregistercodeviceinstallers)已调用)。 特定于设备的共同安装程序不参与以下 DIF 请求：

[**DIF_ALLOW_INSTALL**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-allow-install)

[**DIF_INSTALLDEVICEFILES**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevicefiles)

[**DIF_SELECTBESTCOMPATDRV**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-selectbestcompatdrv)

仅类共同安装程序 （不特定于设备的共同安装程序） 可以响应以下 DIF 请求：

[**DIF_DETECT**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-detect)

[**DIF_FIRSTTIMESETUP**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-firsttimesetup)

[**DIF_NEWDEVICEWIZARD_PRESELECT**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-preselect)

[**DIF_NEWDEVICEWIZARD_SELECT**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-select)

[**DIF_NEWDEVICEWIZARD_PREANALYZE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-preanalyze)

[**DIF_NEWDEVICEWIZARD_POSTANALYZE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-postanalyze)

设备共同安装程序不适合在这些上下文中，是因为尚未确定特定设备或在安装或设备的共同安装程序的早期阶段有尚未注册。

下图显示了该顺序**SetupDiCallClassInstaller**后尚未注册任何特定于设备的共同安装程序会立即调用共同安装程序和类安装程序。

![关系图调用 dif 共同安装程序的请求处理和后续处理](images/callco.png)

在上图所示示例中，两个类共同安装程序注册此设备的安装程序类和一个特定于设备的共同安装程序已注册的设备。 以下步骤对应于在上图中的带圆圈数字：

1.  **SetupDiCallClassInstaller**调用第一类共同安装程序中，指定 DIF 代码，指示正在处理的请求安装 ([**DIF_INSTALLDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevice)，在此示例中)。 辅助安装程序可以选择参与安装请求。 在此示例中，第一个注册的类共同安装程序将返回 NO_ERROR。

2.  **SetupDiCallClassInstaller**，反过来，调用任何其他已注册的类共同安装程序。 在此示例中，第二个类共同安装程序将返回 ERROR_DI_POSTPROCESSING_REQUIRED，请求为后续处理更高版本调用共同安装程序。

3.  **SetupDiCallClassInstaller**调用任何已注册的特定于设备的共同安装程序。

4.  已调用所有已注册的共同安装程序**SetupDiCallClassInstaller**调用系统提供类安装程序中，如果有一个设备的安装程序类。 在此示例中，类安装程序将返回 ERROR_DI_DO_DEFAULT，它是一个典型的返回值，对于类的安装程序。

5.  **SetupDiCallClassInstaller**安装请求调用默认处理程序，如果有的话。 DIF_INSTALLDEVICE 具有默认的处理程序， [ **SetupDiInstallDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)，这是安装程序 Api 的一部分。

6.  **SetupDiCallClassInstaller**调用该请求的后续处理的任何共同安装程序。 在此示例中，第二个类共同安装程序请求的后续处理。

后续处理的辅助安装程序是类似于驱动程序[ **IoCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程，只不过共同安装程序在其单一入口点调用第二次。 当**SetupDiCallClassInstaller**共同安装程序的后续处理调用，它会设置*后续处理*到**TRUE**和*InstallResult*中的相应值*上下文*参数。 在此示例中，*上下文*。*InstallResult*是 NO_ERROR，因为默认处理程序已成功执行。

后续处理，对于**SetupDiCallClassInstaller**按相反的顺序调用共同安装程序。 如果在上图中的所有共同安装程序返回了 ERROR_DI_POSTPROCESSING_REQUIRED， **SetupDiCallClassInstaller**将为后续处理，首先调用 Device_Coinstaller_1 Class_Coinstaller_2 后, 跟和然后 Class_Coinstaller_1。 类安装程序未请求后续处理;仅共同安装程序执行操作。

即使以前的辅助安装程序失败，安装请求调用请求后续处理的共同安装程序。

 

 





