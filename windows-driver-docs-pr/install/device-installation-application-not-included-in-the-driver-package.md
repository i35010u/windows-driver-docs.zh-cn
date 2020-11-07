---
title: 驱动程序包中未包含的设备安装应用程序
description: 不包含在驱动程序包中的设备安装应用程序
ms.assetid: 3c8fd504-50c9-4a61-9cca-cd8cee4e2bd7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4e38c5b480e7dde0be0d66ae398009abeeb20b8
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361497"
---
# <a name="device-installation-application-not-included-in-the-driver-package"></a>不包含在驱动程序包中的设备安装应用程序


此方法描述了一种方法，通过该方法，通过使用 " [完成安装" 操作](finish-install-actions--windows-vista-and-later-.md)，可启动 *设备安装应用程序* 以安装特定于设备的应用程序。

在此方法中，设备安装应用程序不是 [驱动程序包](driver-packages.md)的一部分，并且不使用驱动程序包的 INF 文件将此文件复制到用户的硬盘驱动器。 相反，共同安装程序会直接从分发介质启动设备安装应用程序，或提示用户从 Internet 下载设备安装应用程序。

此方法具有以下优点：

-   如果共同安装程序提供了 " [完成-安装" 操作](finish-install-actions--windows-vista-and-later-.md)，则可以使用此方法在 windows Vista 和更高版本的 windows 上安装 [驱动程序包](driver-packages.md) 和设备特定的应用程序。

-   只有驱动程序包才能进行数字签名。 设备安装应用程序和关联的安装文件无需进行数字签名。 有关数字签名的详细信息，请参阅 [驱动程序签名](driver-signing.md)。

-   仅将驱动程序包复制到驱动程序存储区。 启动设备安装应用程序时，设备特定的应用程序将安装在用户的硬盘驱动器上的其他位置。

-   可以在 [驱动程序包](driver-packages.md) 更新过程中提示用户更新设备特定的应用程序。 此操作通过包的共同安装程序提供的 " [完成安装" 操作](finish-install-actions--windows-vista-and-later-.md) 进行。 通过这种方式，驱动程序包和特定于设备的应用程序的同步版本是可选的。 另外，还可以从 Internet 下载其他设备特定的应用程序，这些应用程序不在分发介质上。

-   独立硬件供应商 (IHV) 具有更大的分发介质灵活性。 设备安装应用程序和设备特定的应用程序可以在介质上，也可以从 Internet 下载。

如果使用此方法，则每当用户在插入分发媒体之前安装设备，或 Windows 更新检测到设备的新驱动程序时，将发生以下情况：

1.  设备的 [驱动程序包](driver-packages.md) 已安装，如 [硬件优先安装](hardware-first-installation.md)中所述。

2.  如果驱动程序包的共同安装程序提供了 " [完成-安装" 操作](finish-install-actions--windows-vista-and-later-.md)，则驱动程序包安装结束时会发生以下情况之一：

    -   分发介质上的设备安装应用程序用于安装特定于设备的应用程序。
    -   系统将提示用户从 Internet 下载设备安装应用程序的较新版本。 通过这一点，IHV 可以提供其他设备特定的应用程序，这些应用程序不在分发介质上。

        然后，在从 Internet 下载设备安装应用程序后立即启动该应用程序。

**注意**  由于在启动设备安装应用程序之前已安装了 [驱动程序包](driver-packages.md) ，因此应用程序必须检测是否已安装驱动程序，并且仅安装设备特定的应用程序。

 

有关共同安装程序的详细信息，请参阅 [编写共同安装程序](writing-a-co-installer.md)。

有关通过共同安装程序启动设备安装应用程序的详细信息，请参阅 [通过共同安装程序启动设备安装应用程序的指南](guidelines-for-starting-device-installation-applications-through-co-in.md)。

 

 





