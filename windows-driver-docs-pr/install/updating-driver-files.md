---
title: 更新驱动程序文件
description: 更新驱动程序文件
ms.assetid: e232abd9-4e51-4fa7-a00c-f5e184706222
keywords:
- 硬件更新向导 WDK
- 更新驱动程序文件
- 驱动程序文件更新 WDK
- 设备安装程序 WDK 设备安装，更新现有的驱动程序
- 设备安装 WDK，更新现有的驱动程序
- 安装设备 WDK，更新现有的驱动程序
- WDK 的现有驱动程序更新
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc88fa941c2245549fabece328b822f252a58bce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563685"
---
# <a name="updating-driver-files"></a>更新驱动程序文件





出现以下情况之一时，会更新驱动程序：

-   **硬件更新向导**从运行**设备管理器**。

    **请注意**  从 Windows Vista 开始，此向导现在名为**更新驱动程序软件向导**。

     

-   运行 Windows 更新。

-   运行安装软件的设备。

-   从 Windows Vista 开始，你可以运行[PnPUtil](https://msdn.microsoft.com/library/windows/hardware/ff550419)工具从提升的命令提示符来安装或更新[驱动程序包](driver-packages.md)设备。

在编写安装软件和更新现有的驱动程序的 INF 文件时，请使用以下指导原则。

-   安装软件可以调用[ **UpdateDriverForPlugAndPlayDevices**](https://msdn.microsoft.com/library/windows/hardware/ff553534)，提供一个 INF 文件和硬件 ID，若要更新的与硬件 ID 匹配的设备驱动程序

    从 Windows Vista 开始，安装软件还可以调用以下操作来更新驱动程序之一：

    -   [**DiInstallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff544717)，其中预安装的驱动程序，然后在驱动程序支持的系统中存在的设备上安装驱动程序。
    -   [**DiInstallDevice**](https://msdn.microsoft.com/library/windows/hardware/ff544710)，这将指定的驱动程序安装从系统中的指定设备上的驱动程序存储。

    有关详细信息，请参阅[编写设备安装应用程序](writing-a-device-installation-application.md)。

-   当升级驱动程序，类安装程序和共同安装程序不应提供在响应中的完成安装页[ **DIF_NEWDEVICEWIZARD_FINISHINSTALL** ](https://msdn.microsoft.com/library/windows/hardware/ff543702)除非绝对必要。 如果可能，请从以前安装的设置获取完成安装信息。

-   可能的范围内，安装程序类和共同安装程序应避免使基于它们所提供的初始安装还是要更新已安装的设备驱动程序的行为。

-   从 Windows XP 中，注册表值**CoInstallers32**并**EnumPropPages32**之前的交付删除[ **DIF_REGISTER_COINSTALLERS**](https://msdn.microsoft.com/library/windows/hardware/ff543715). 对于较早的操作系统版本的 INF 文件必须显式删除这些值或执行 nonappending 修改它们的操作。

-   从 Windows XP 中，注册表值**上边的筛选程序**并**下边的筛选程序**之前的交付删除[ **DIF_INSTALLDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff543692). 对于较早的操作系统版本的 INF 文件必须显式删除这些值或执行 nonappending 修改它们的操作。

-   不要*不*使用[ **INF DelFiles 指令**](inf-delfiles-directive.md)或者[ **INF RenFiles 指令**](inf-renfiles-directive.md)更新时驱动程序。 Windows 不能保证不使用特定文件的另一台设备。 (安装程序类和共同安装程序可以删除或重命名文件，*如果*它们能够可靠地确定没有设备正在使用的文件。)

-   使用[ **INF DelReg 指令**](inf-delreg-directive.md)若要从以前安装的设备，删除旧的设备特定的注册表项，如果不再需要的条目。 （不删除全局注册表项。）

-   不要*不*使用[ **INF DelService 指令**](inf-delservice-directive.md)中[ **INF DDInstall.Services 部分**](inf-ddinstall-services-section.md)到从目标计算机中删除以前安装的设备/驱动程序服务。 Windows 不能保证不使用特定服务的另一台设备。 (安装程序类和共同安装程序可以删除服务，*如果*它们能够可靠地确定没有设备正在使用的服务。)

-   当更新安装程序类、 类共同安装程序或服务 DLL 时，必须为新版本提供新的文件名。

有关 INF 文件的详细信息，请参阅[创建一个 INF 文件](overview-of-inf-files.md)并[INF 文件的部分和指令](inf-file-sections-and-directives.md)。

 

 





