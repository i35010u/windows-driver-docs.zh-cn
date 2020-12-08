---
title: 辅助安装程序操作
description: 辅助安装程序操作
keywords:
- 共同安装程序的 WDK 设备安装，其工作原理
- 共同安装程序 WDK 设备安装，示例
- SetupDiCallClassInstaller
- 类共同安装程序 WDK
- DIF 请求共同安装程序示例 WDK
- 设备特定的共同安装程序 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 510681db637737ceee722733b667b72b7243aa93
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827959"
---
# <a name="co-installer-operation"></a>辅助安装程序操作





Setupapi.log 调用共同安装程序，如下图所示。

![阐释共同安装程序如何参与设备安装的关系图](images/coinsts.png)

Unshaded 框表示操作系统为 [系统提供的设备安装程序类](/windows-hardware/drivers/install/system-defined-device-setup-classes-reserved-for-system-use)提供的组件。 着色框表示您可以提供的组件。 如果创建自定义设备安装程序类，还可以提供类安装程序。 但是，很少需要创建新的设备安装程序类，因为几乎每个设备都可以与系统提供的设备安装程序类之一相关联。 有关 Windows 组件的详细信息，请参阅 [设备安装概述](overview-of-device-and-driver-installation.md)。

可以为特定设备提供 (*设备特定的共同安装程序*) 或 (*类共同安装* 程序) 的设备安装程序类的共同安装程序。 仅当安装为其注册了共同安装程序的设备时，Setupapi.log 才会调用设备特定的共同安装程序。 操作系统和供应商可以为设备注册零个或多个特定于设备的共同安装程序。 当安装为其注册了共同安装程序的设备安装程序类的任何设备时，Setupapi.log 会调用类共同安装程序。 操作系统和供应商可以为设备安装程序类注册一个或多个类共同安装程序。 此外，可以为一个或多个安装程序类注册类共同安装程序。

Windows 和 [自定义设备安装应用程序](writing-a-device-installation-application.md)通过使用 [设备安装函数代码](/previous-versions/ff541307(v=vs.85))调用 [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller)来安装设备，)  (DIF 代码。

在 GUI 模式安装过程中，操作系统通过 DIF 代码调用 [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller) ，以检测系统中存在的非 PnP 设备。 IHV 通常会提供共同安装程序，为 IHV 发布的非 PnP 设备执行此操作。

对于每个 DIF 请求， **SetupDiCallClassInstaller** 会调用注册到设备的安装程序类的任何类共同安装程序、为特定设备注册的任何设备共同安装程序，以及系统为设备的安装程序类提供的类安装程序（如果有）。

自定义设备安装应用程序必须调用 **SetupDiCallClassInstaller** ，而不是直接调用共同安装程序或类安装程序。 此函数可确保正确调用所有注册的共同安装程序。

类共同安装程序通常在安装设备之前注册，设备特定的共同安装程序将注册为设备安装的一部分。 因此，在设备安装过程中，类共同安装程序通常会被添加到共同安装程序列表，并为所有 DIF 请求调用。

为设备 (或 [**SetupDiRegisterCoDeviceInstallers**](/windows/win32/api/setupapi/nf-setupapi-setupdiregistercodeviceinstallers)调用了) [**DIF_REGISTER_COINSTALLERS**](./dif-register-coinstallers.md)后，操作系统会将特定于设备的共同安装程序添加到共同安装程序列表中。 设备特定的共同安装程序不参与以下 DIF 请求：

[**DIF_ALLOW_INSTALL**](./dif-allow-install.md)

[**DIF_INSTALLDEVICEFILES**](./dif-installdevicefiles.md)

[**DIF_SELECTBESTCOMPATDRV**](./dif-selectbestcompatdrv.md)

只有类共同安装程序 (不是特定于设备的共同安装程序) 可以响应以下 DIF 请求：

[**DIF_DETECT**](./dif-detect.md)

[**DIF_FIRSTTIMESETUP**](./dif-firsttimesetup.md)

[**DIF_NEWDEVICEWIZARD_PRESELECT**](./dif-newdevicewizard-preselect.md)

[**DIF_NEWDEVICEWIZARD_SELECT**](./dif-newdevicewizard-select.md)

[**DIF_NEWDEVICEWIZARD_PREANALYZE**](./dif-newdevicewizard-preanalyze.md)

[**DIF_NEWDEVICEWIZARD_POSTANALYZE**](./dif-newdevicewizard-postanalyze.md)

在这些上下文中，设备共同安装程序并不适用，这是因为尚未标识特定设备或在此早期安装阶段，或者尚未注册设备共同安装程序。

下图显示了在注册了任何特定于设备的共同安装程序后， **SetupDiCallClassInstaller** 调用共同安装程序和类安装程序的顺序。

![为 dif 请求处理和后处理调用共同安装程序的示意图](images/callco.png)

在上图所示的示例中，为此设备的安装程序类注册了两个类共同安装程序，并为该设备注册了一个特定于设备的共同安装程序。 以下步骤与上图中的带圆圈数字相对应：

1.  **SetupDiCallClassInstaller** 调用第一个类共同安装程序，并指定一个 DIF 代码，该代码指示正在处理 ([**DIF_INSTALLDEVICE**](./dif-installdevice.md)的安装请求，在此示例) 。 共同安装程序可以选择参与安装请求。 在此示例中，第一个注册的类共同安装程序返回 NO_ERROR。

2.  反过来， **SetupDiCallClassInstaller** 调用任何其他注册的类共同安装程序。 在此示例中，第二个类共同安装程序返回 ERROR_DI_POSTPROCESSING_REQUIRED，这会要求稍后调用共同安装程序进行后处理。

3.  **SetupDiCallClassInstaller** 将调用任何注册的设备特定的共同安装程序。

4.  在调用了所有已注册的共同安装程序后， **SetupDiCallClassInstaller** 将调用系统提供的类安装程序（如果设备的安装程序类有一个安装程序）。 在此示例中，类安装程序返回 ERROR_DI_DO_DEFAULT，这是类安装程序的典型返回值。

5.  **SetupDiCallClassInstaller** 调用安装请求的默认处理程序（如果有）。 DIF_INSTALLDEVICE 具有默认处理程序 [**SetupDiInstallDevice**](/windows/win32/api/setupapi/nf-setupapi-setupdiinstalldevice)，它是 setupapi.log 的一部分。

6.  **SetupDiCallClassInstaller** 调用请求后处理的所有共同安装程序。 在此示例中，第二个类共同安装程序请求了后处理。

共同安装程序的后处理类似于 driver [**IoCompletion**](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，只是在它的单个入口点调用了共同安装程序。 当 **SetupDiCallClassInstaller** 调用共同安装程序进行后处理时，它会将 *后处理* 设置为 **TRUE** ，并将 *InstallResult* 设置为 *上下文* 参数中的相应值。 在此示例中为 *上下文*。*InstallResult* 是 NO_ERROR 的，因为默认处理程序已成功执行。

对于后处理， **SetupDiCallClassInstaller** 以相反顺序调用共同安装程序。 如果上图中的所有共同安装程序都已返回 ERROR_DI_POSTPROCESSING_REQUIRED，则 **SetupDiCallClassInstaller** 将先调用 Device_Coinstaller_1 进行后处理，然后再执行 Class_Coinstaller_2，然后 Class_Coinstaller_1。 类安装程序不请求后处理;仅限共同安装程序。

即使之前的共同安装程序未能安装请求，也会调用请求后处理的共同安装程序。

 

