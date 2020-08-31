---
title: 设备安装应用程序编写指南
description: 设备安装应用程序编写指南
ms.assetid: 7f364b95-98ca-479a-8cdb-5e5e77c70cfa
keywords:
- 安装应用程序 WDK，指导原则
- 设备安装应用程序 WDK，指导原则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8087da366ec9640d966ac1c58605c1ca80f9fe8c
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095323"
---
# <a name="guidelines-for-writing-device-installation-applications"></a>设备安装应用程序编写指南


*设备安装应用程序*   *必须* 执行以下操作：

-   支持删除其安装的所有设备特定的应用程序。 在卸载过程中，设备安装应用程序应检查系统上是否仍然存在任何关联的设备，如果是，则警告用户。

-   遵循在 [64 位系统上安装设备](device-installations-on-64-bit-systems.md)的准则。

-   从 Windows Vista 开始，列出通过使用 Microsoft Windows Installer (MSI) 安装的所有应用程序，以及 "控制面板" 的 " **程序和功能** " 中可用的应用程序。 然后，你可以根据需要卸载这些项。

-   在早于 Windows Vista 的 Windows 版本中，列出了通过使用 Microsoft Windows Installer (MSI) 安装的所有应用程序，并在 "控制面板" 的 " **添加或删除程序** " 中提供了这些应用程序。 然后，你可以根据需要卸载这些项。

-   遵循 Microsoft Windows 应用程序的准则。 有关详细信息，请参阅 [Microsoft 开发人员网络](https://go.microsoft.com/fwlink/p/?linkid=8714) 网站。

设备安装应用程序 *可以* 执行以下操作：

-   [安装特定于设备的应用程序](installing-device-specific-applications.md)

    **注意**   我们强烈建议你将特定于设备的应用程序提交到适用于软件[ (HCK) 的适当硬件认证工具包](https://go.microsoft.com/fwlink/p/?linkid=227016)。 有关详细信息，请参阅 [Microsoft 开发人员网络](https://go.microsoft.com/fwlink/p/?linkid=8714) 网站。

     

-   [预载驱动程序包](preloading-driver-packages.md)

-   [预安装驱动程序包](preinstalling-driver-packages.md)

设备安装应用程序 *不能* 执行以下操作：

-   指示用户复制或覆盖任何文件，尤其是。*inf* 和。*sys* 文件。

-   在卸载操作期间从系统中删除已安装的驱动程序文件，即使删除了硬件也是如此。

-   强制任何不必要的系统重新启动。 安装 PnP 设备或软件应用程序通常不需要重新启动。 [**UpdateDriverForPlugAndPlayDevices**](/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)函数的*bRebootRequired*参数表示需要重新启动。

-   使用 RunOnce 注册表项，因为这需要重新启动系统。

-   使用设备或类共同安装程序或类安装程序来启动设备安装应用程序，因为在设备安装过程中系统的状态无法保证在安装软件应用程序时是安全的。 具体而言，如果设备安装应用程序在服务器端安装过程中运行，系统将停止响应。

    安装设备后，可以通过使用由类安装程序或共同安装程序提供的 " [完成-安装" 操作](finish-install-actions--windows-vista-and-later-.md) 来安全地启动设备安装应用程序。

    有关共同安装程序的详细信息，请参阅 [编写共同安装程序](writing-a-co-installer.md)。

-   使用 "启动" 组启动 *设备安装应用程序*。

-   使用 *win.ini* 条目开始设备安装应用程序。

-   强制用户安装任何设备特定的应用程序，除非该设备在没有应用程序的情况下将无法运行。 例如，如果收件箱应用程序不支持此类功能，则可能包括用于设置可配置键盘密钥或设置调制解调器的国家/地区代码的实用程序。

 

