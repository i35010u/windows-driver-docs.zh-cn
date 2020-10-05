---
title: 使用 SetupAPI 卸载设备和驱动程序包
description: 使用 SetupAPI 卸载设备和驱动程序包
ms.assetid: e170961b-5d12-43d5-b502-3b37e6421f6e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf6468f6b12155ba22b076b16581a87ed0a22a50
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732729"
---
# <a name="using-setupapi-to-uninstall-devices-and-driver-packages"></a>使用 SetupAPI 卸载设备和驱动程序包


[Setupapi.log](setupapi.md) 是提供两组函数的系统组件：

-   [常规设置函数](/previous-versions/ff544985(v=vs.85))

-   [设备安装功能](/previous-versions/ff541299(v=vs.85))

*设备安装应用程序*、 *共同安装*程序和 *类* 安装程序可以使用这些功能来执行设备安装的自定义操作。 Setupapi.log 还支持卸载它所安装的设备和 [驱动程序包](driver-packages.md) 。

本主题介绍了使用 Setupapi.log 函数卸载设备和驱动程序包时可以遵循的过程。

有关卸载驱动程序包和驱动程序包的详细信息，请参阅 [如何卸载设备和驱动程序包](how-devices-and-driver-packages-are-uninstalled.md)。

### <a name="uninstalling-the-device"></a><a href="" id="uninstalling-the-device"></a> 卸载设备

使用以下方法从系统中 Setupapi.log) ：

-   设备安装应用程序可以通过调用 [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller) 函数来请求卸载设备。 当应用程序调用此函数以卸载设备时，它必须将 *InstallFunction* 参数设置为 [**DIF_REMOVE**](./dif-remove.md) 代码。  有关所有 DIF 代码的列表，请参阅 [设备安装函数](/previous-versions/ff541307(v=vs.85))。

    如果在 DIF_REMOVE 请求的处理过程中调用 [**SetupDiRemoveDevice**](/windows/win32/api/setupapi/nf-setupapi-setupdiremovedevice) ，则该函数将从系统中删除设备的 devnode。 它还会删除设备的硬件和软件注册表项，以及任何特定于硬件配置文件的注册表项， () 特定于配置的注册表项。

    **请注意**，  **SetupDiRemoveDevice**只能由类安装程序调用，而不能由设备安装应用程序调用。

    有关 DIF 代码的详细信息，请参阅 [处理 Dif 代码](handling-dif-codes.md)。

-   从 Windows 7 开始，设备安装应用程序可以通过调用 [**DiUninstallDevice**](/windows/win32/api/newdev/nf-newdev-diuninstalldevice) 函数来卸载设备。 此函数类似于调用 [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller) ，并将 *InstallFunction* 参数设置为 [**DIF_REMOVE**](./dif-remove.md)。 但是，除了删除指定设备的 devnode 以外，此函数还将尝试删除在调用时系统上存在的设备的所有子 devnodes。

### <a name="deleting-a-driver-package-from-the-driver-store"></a><a href="" id="deleting-a-driver-package-from-the-driver-store"></a> 从驱动程序存储区中删除驱动程序包

从 Windows XP 开始，设备安装应用程序可以调用 [SetupUninstallOEMInf](/windows/win32/api/setupapi/nf-setupapi-setupuninstalloeminfa) 函数从系统 inf 文件目录中删除指定的 [INF 文件](overview-of-inf-files.md) 。

从 Windows Vista 开始，此函数还将从[驱动程序存储区](driver-store.md)中删除包含指定 INF 文件的[驱动程序包](driver-packages.md)。

### <a name="deleting-the-binary-files-of-the-installed-driver"></a><a href="" id="deleting-the-binary-files-of-the-installed-driver"></a> 正在删除已安装驱动程序的二进制文件

Setupapi.log 无法用于执行此操作。

