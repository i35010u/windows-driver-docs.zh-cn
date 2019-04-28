---
title: 使用 SetupAPI 卸载设备和驱动程序包
description: 使用 SetupAPI 卸载设备和驱动程序包
ms.assetid: e170961b-5d12-43d5-b502-3b37e6421f6e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f460b6b4ff6229bfc8a55e127388669f6a84f16
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339398"
---
# <a name="using-setupapi-to-uninstall-devices-and-driver-packages"></a>使用 SetupAPI 卸载设备和驱动程序包


[SetupAPI](setupapi.md)是提供两组函数的系统组件：

-   [常规设置函数](https://msdn.microsoft.com/library/windows/hardware/ff544985)

-   [设备安装函数](https://msdn.microsoft.com/library/windows/hardware/ff541299)

*设备安装应用程序*，*共同安装程序*，和*类安装程序*可以使用这些函数执行的设备安装的自定义操作。 安装程序 Api 还支持卸载设备和[驱动程序包](driver-packages.md)的安装。

本主题介绍了可以按照使用 SetupAPI 函数卸载设备和驱动程序包的过程。

有关卸载驱动程序和驱动程序包的详细信息，请参阅[卸载如何设备和驱动程序包](how-devices-and-driver-packages-are-uninstalled.md)。

### <a href="" id="uninstalling-the-device"></a> 卸载设备

安装程序 Api) 从系统使用以下方法：

-   设备安装应用程序可以请求设备通过调用卸载[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)函数。 当应用程序调用此函数可卸载设备时，它必须设置*InstallFunction*参数[ **DIF_REMOVE** ](https://msdn.microsoft.com/library/windows/hardware/ff543717)代码。  有关所有 DIF 代码的列表，请参阅[设备安装函数](https://msdn.microsoft.com/library/windows/hardware/ff541307)。

    如果[ **SetupDiRemoveDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff552097)调用期间 DIF_REMOVE 请求的处理，该函数会设备的 devnode 从系统中。 它还会删除设备的硬件和软件的注册表项，以及任何特定于硬件的配置文件的注册表项 （特定于配置的注册表项）。

    **请注意**  **SetupDiRemoveDevice**只能由类安装程序而不是设备安装应用程序调用。

    有关差异代码的详细信息，请参阅[处理 DIF 代码](handling-dif-codes.md)。

-   从 Windows 7 开始，设备安装应用程序可以卸载设备通过调用[ **DiUninstallDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff544754)函数。 此函数是类似于调用[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)与*InstallFunction*参数设置为[ **DIF_REMOVE**](https://msdn.microsoft.com/library/windows/hardware/ff543717). 但是，除了删除指定的设备的 devnode，此函数尝试删除的设备是在调用时在系统上存在的所有子 devnodes。

### <a href="" id="deleting-a-driver-package-from-the-driver-store"></a> 从驱动程序存储区中删除驱动程序包

从 Windows XP 开始，设备安装应用程序可以调用[SetupUninstallOEMInf](https://go.microsoft.com/fwlink/p/?linkid=169503)函数来删除指定[INF 文件](inf-files.md)从系统 INF 文件目录。

从 Windows Vista 开始，此函数还会删除[驱动程序包](driver-packages.md)，其中包含指定的 INF 文件，从[驱动程序存储区](driver-store.md)。

### <a href="" id="deleting-the-binary-files-of-the-installed-driver"></a> 删除已安装的驱动程序的二进制文件

安装程序 Api 不能用于执行此操作。

 

 





