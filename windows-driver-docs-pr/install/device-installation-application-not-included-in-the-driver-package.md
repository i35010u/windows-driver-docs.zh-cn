---
title: 不包含驱动程序包中的设备安装应用程序
description: 不包含在驱动程序包中的设备安装应用程序
ms.assetid: 3c8fd504-50c9-4a61-9cca-cd8cee4e2bd7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8386c1bb6ece9d68be9e7c032cfff8cf9744adc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357939"
---
# <a name="device-installation-application-not-included-in-the-driver-package"></a>不包含在驱动程序包中的设备安装应用程序


此方法介绍了通过该共同安装程序中，通过使用完成安装操作来安装特定于设备的应用程序的方法。

在此方法中，设备安装应用程序不是属于[驱动程序包](driver-packages.md)，和驱动程序包的 INF 文件不用于此文件复制到用户的硬盘。 相反，辅助安装程序直接从分发介质中，启动设备安装应用程序或提示用户从 Internet 下载的设备安装应用程序。

此方法具有以下优点：

-   如果共同安装程序提供[完成安装操作](finish-install-actions--windows-vista-and-later-.md)，此方法可用于安装[驱动程序包](driver-packages.md)和 Windows Vista 和更高版本的 Windows 上的特定于设备的应用程序。

-   仅对驱动程序包必须进行数字签名。 设备安装应用程序和关联的安装文件无需进行数字签名。 有关数字签名的详细信息，请参阅[驱动程序签名](driver-signing.md)。

-   仅对驱动程序包复制到驱动程序存储区中。 设备安装应用程序启动时，特定于设备的应用程序是在其他地方安装在用户的硬盘上。

-   可以在系统提示用户[驱动程序包](driver-packages.md)更新来更新特定于设备的应用程序。 通过将发生这种情况[完成安装操作](finish-install-actions--windows-vista-and-later-.md)提供的包的辅助安装程序。 这样一来，同步版本的驱动程序包和特定于设备的应用程序是可选的。 此外，其他特定于设备的应用程序，不在分发介质，可以从 Internet 下载。

-   独立硬件供应商 (IHV) 具有更灵活地进行分发介质。 设备安装应用程序和特定于设备的应用程序可以是媒体上，也可以从 Internet 下载。

如果使用此方法，将进行以下操作每次用户插入分发介质之前安装该设备或 Windows 更新检测到设备的新驱动程序：

1.  [驱动程序包](driver-packages.md)中所述安装设备[硬件第一个安装](hardware-first-installation.md)。

2.  如果驱动程序包的共同安装程序提供[完成安装操作](finish-install-actions--windows-vista-and-later-.md)，驱动程序的包安装结束时以下项之一发生：

    -   启动分发介质上的设备安装应用程序以安装特定于设备的应用程序。
    -   提示用户从 Internet 下载的设备安装应用程序的较新版本。 通过此方法，IHV 可以提供不分发介质上的其他特定于设备的应用程序。

        辅助安装程序然后启动设备安装应用程序，只要它从 Internet 下载。

**请注意**  由于[驱动程序包](driver-packages.md)已安装的设备安装应用程序在启动之前，应用程序必须检测驱动程序已安装，并仅安装特定于设备的应用程序。

 

有关共同安装程序的详细信息，请参阅[编写共同安装程序](writing-a-co-installer.md)。

有关启动通过共同安装程序的设备安装应用程序的详细信息，请参阅[共同安装程序通过启动设备安装的应用程序指南](guidelines-for-starting-device-installation-applications-through-co-in.md)。

 

 





