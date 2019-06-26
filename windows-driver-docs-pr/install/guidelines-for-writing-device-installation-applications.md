---
title: 设备安装应用程序编写指南
description: 设备安装应用程序编写指南
ms.assetid: 7f364b95-98ca-479a-8cdb-5e5e77c70cfa
keywords:
- 安装应用程序 WDK，准则
- 设备安装应用程序 WDK，准则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd25f55a13798c46185113374933264294c157b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383842"
---
# <a name="guidelines-for-writing-device-installation-applications"></a>设备安装应用程序编写指南


*设备安装应用程序*   *必须*执行以下操作：

-   支持在安装的所有特定于设备的应用程序中删除。 过程中的卸载过程，如设备安装应用程序应检查是否任何关联的设备仍存在系统上并且，如果是这样，警告用户。

-   遵循的准则[64 位系统上安装设备](device-installations-on-64-bit-systems.md)。

-   从 Windows Vista 开始列出的已使用 Microsoft Windows Installer (MSI) 安装以及可在所有应用程序**程序和功能**控制面板中。 然后，如有必要，可以卸载这些项。

-   在版本的 Windows 早于 Windows Vista，列出所有通过使用 Microsoft Windows Installer (MSI) 安装和中提供的应用程序**添加或删除程序**控制面板中。 然后，如有必要，可以卸载这些项。

-   请按照 Microsoft Windows 应用程序的准则。 请参阅[Microsoft Developer Network](https://go.microsoft.com/fwlink/p/?linkid=8714)网站以获取更多信息。

设备安装应用程序*可以*执行以下操作：

-   [安装特定于设备的应用程序](installing-device-specific-applications.md)

    **请注意**  我们强烈建议提交到相应的特定于设备的应用程序[硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)软件。 请参阅[Microsoft Developer Network](https://go.microsoft.com/fwlink/p/?linkid=8714)网站以获取更多信息。

     

-   [预加载的驱动程序包](preloading-driver-packages.md)

-   [预安装的驱动程序包](preinstalling-driver-packages.md)

设备安装应用程序*不得*执行以下操作：

-   指示要复制或覆盖任何文件，尤其是用户。*inf*和。*sys*文件。

-   已安装的驱动程序文件从系统中删除在卸载操作时，即使该硬件被删除。

-   强制执行任何不必要的系统重启。 重启通常不是安装即插即用设备或软件应用程序所必需的。 *BRebootRequired*的参数[ **UpdateDriverForPlugAndPlayDevices** ](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)函数指示需要重新启动。

-   使用 RunOnce 注册表项，因为这需要重启系统。

-   使用设备类共同安装程序或类安装程序中，若要启动设备安装应用程序，因为不能保证在设备安装过程中系统的状态是安全的安装软件应用程序。 具体而言，如果设备安装应用程序运行在服务器端安装期间，系统将停止响应。

    安装设备后，可以安全地启动设备安装应用程序通过使用[完成安装操作](finish-install-actions--windows-vista-and-later-.md)由类安装程序或共同安装程序提供的。

    有关共同安装程序的详细信息，请参阅[编写共同安装程序](writing-a-co-installer.md)。

-   使用启动组启动*设备安装应用程序*。

-   使用*win.ini*条目以启动设备安装应用程序。

-   强制用户安装特定于设备的任何应用程序，除非设备将无法运行而无需应用程序。 示例可能包括用于设置可配置的键盘键或用于设置调制解调器的国家/地区代码的实用程序，如果收件箱应用程序不支持此类功能。

 

 





