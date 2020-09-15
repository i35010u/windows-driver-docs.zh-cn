---
title: 更新驱动程序文件
description: 更新驱动程序文件
ms.assetid: e232abd9-4e51-4fa7-a00c-f5e184706222
keywords:
- 硬件更新向导 WDK
- 正在更新驱动程序文件
- 驱动程序文件更新 WDK
- 设备设置 WDK 设备安装，更新现有驱动程序
- 设备安装 WDK，更新现有驱动程序
- 安装设备 WDK，更新现有驱动程序
- 现有驱动程序更新 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bba10201ec53a2d07988a3c9af62cfa131abcf8c
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107332"
---
# <a name="updating-driver-files"></a>更新驱动程序文件





每当发生以下情况之一时，就会更新驱动程序：

-   将从**设备管理器**运行**硬件更新向导**。

    **注意**   从 Windows Vista 开始，此向导现在命名为 "**更新驱动程序软件向导**"。

     

-   运行 Windows 更新。

-   设备的安装软件已运行。

-   从 Windows Vista 开始，你可以从提升的命令提示符运行 [PnPUtil](../devtest/pnputil.md) 工具，以便安装或更新设备的 [驱动程序包](driver-packages.md) 。

编写更新现有驱动程序的安装软件和 INF 文件时，请使用以下准则。

-   安装软件可以调用 [**UpdateDriverForPlugAndPlayDevices**](/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)（提供 INF 文件和硬件 id）来更新与硬件 id 匹配的设备的驱动程序。

    从 Windows Vista 开始，安装软件还可以调用以下项之一来更新驱动程序：

    -   [**DiInstallDriver**](/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)，它预安装驱动程序，然后将驱动程序安装在驱动程序支持的系统中的设备上。
    -   [**DiInstallDevice**](/windows/desktop/api/newdev/nf-newdev-diinstalldevice)，它从系统中存在的指定设备上的驱动程序存储区中安装指定的驱动程序。

    有关详细信息，请参阅 [编写设备安装应用程序](writing-a-device-installation-application.md)。

-   升级驱动程序时，类安装程序和共同安装程序不应提供 "完成-安装" 页来响应 [**DIF_NEWDEVICEWIZARD_FINISHINSTALL**](./dif-newdevicewizard-finishinstall.md) ，除非绝对必要。 如果可能，请从上一安装的设置中获取 "完成-安装" 信息。

-   在可能的情况下，类安装程序和共同安装程序应避免依赖于是否提供初始安装或正在为已安装的设备更新驱动程序。

-   从 Windows XP 开始，将在[**DIF_REGISTER_COINSTALLERS**](./dif-register-coinstallers.md)传递之前删除注册表值**CoInstallers32**和**EnumPropPages32** 。 对于早期版本的操作系统版本，INF 文件必须显式删除这些值或对这些值执行 nonappending 修改操作。

-   从 Windows XP 开始，将在[**DIF_INSTALLDEVICE**](./dif-installdevice.md)传递之前删除注册表值**UpperFilters**和**LowerFilters** 。 对于早期版本的操作系统版本，INF 文件必须显式删除这些值或对这些值执行 nonappending 修改操作。

-   更新驱动程序时， *不要使用* [**inf DelFiles 指令**](inf-delfiles-directive.md) 或 [**inf RenFiles 指令**](inf-renfiles-directive.md) 。 Windows 无法保证特定文件未被其他设备使用。  (类安装程序和共同安装程序可以删除或重命名文件， *前提* 是它们可以可靠地确定没有设备使用这些文件。 ) 

-   如果不再需要这些项，请使用 [**INF DelReg 指令**](inf-delreg-directive.md) 从以前安装的设备中删除旧的特定于设备的注册表项。  (不删除全局注册表项。 ) 

-   请勿*在* [**inf DDInstall 部分**](inf-ddinstall-services-section.md)中使用[**inf DelService 指令**](inf-delservice-directive.md)从目标计算机中删除以前安装的设备/驱动程序服务。 Windows 无法保证特定的服务未被其他设备使用。  (类安装程序和共同安装程序可以删除服务， *前提* 是它们可以可靠地确定没有设备在使用服务。 ) 

-   更新类安装程序、类共同安装程序或服务 DLL 时，必须为新版本指定一个新的文件名。

有关 INF 文件的详细信息，请参阅 [创建 Inf 文件](overview-of-inf-files.md) 和 [inf 文件部分和指令](./index.md)。

