---
title: 驱动程序包中包含的设备安装应用程序
description: 包含在驱动程序包中的设备安装应用程序
ms.assetid: bd6e182c-6b7a-4cde-bcc7-637ae6bf39be
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0be1de27f776b43a280c1757264c611f7d40015d
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361307"
---
# <a name="device-installation-application-that-is-included-in-the-driver-package"></a>包含在驱动程序包中的设备安装应用程序


此方法描述了一种方法，通过该方法，使用 " [完成安装" 操作](finish-install-actions--windows-vista-and-later-.md)的共同安装 *程序可以启动设备安装应用程序* 以安装特定于设备的应用程序。

在此方法中，设备安装应用程序和关联的安装文件是 [驱动程序包](driver-packages.md)的一部分，驱动程序包的 INF 文件用于将应用程序和安装文件复制到驱动程序存储区。 因此，应用程序和驱动程序都已安装在所有方案中。

此方法具有以下优点：

-   如果共同安装程序提供了 [完成安装操作](finish-install-actions--windows-vista-and-later-.md)，则可以使用此方法在 windows Vista 和更高版本的 windows 上安装驱动程序包，包括特定于设备的应用程序。

-   由于设备安装应用程序、关联的安装文件和驱动程序是同一驱动程序包的一部分，因此将同时安装或更新它们。 这会同步驱动程序包中所有组件的版本。

但是，此方法也具有以下缺点：

-   如果设备安装应用程序和关联的安装文件属于 [驱动程序包](driver-packages.md)，则必须对其进行数字签名。 有关数字签名的详细信息，请参阅 [驱动程序签名](driver-signing.md)。

    此外，每当修改这些组件时，驱动程序、设备安装应用程序和关联的安装文件必须提交给 Windows 硬件质量实验室 (WHQL) 为单个驱动程序包。 有关此过程的详细信息，请参阅 [WHQL 发行版签名](whql-release-signature.md)。

-   设备安装应用程序和关联的安装文件将复制到用户硬盘上的两个位置：驱动程序存储区，以及在 INF 文件的 [**Inf DestinationDirs 部分**](inf-destinationdirs-section.md)中指定的目录。

-   不能通过设备安装应用程序安装的可选设备特定应用程序无法从分发介质安装或从 Internet 下载。

    由于设备安装应用程序和关联的安装文件已签名为 [驱动程序包](driver-packages.md)的一部分，因此只允许通过设备安装应用程序安装的应用程序来确保驱动程序包的完整性。

如果使用此方法，则每当用户在插入分发媒体之前安装设备，或 Windows 更新检测到设备的新驱动程序时，将发生以下情况：

1.  设备的驱动程序包已安装，如 [硬件优先安装](hardware-first-installation.md)中所述。

2.  [驱动程序包的](driver-packages.md)INF 文件将设备安装应用程序和关联安装文件复制到用户硬盘上的目录中，该目录通常是 Program files 目录。 这是在 INF 文件中处理 [**Inf CopyFiles 指令**](inf-copyfiles-directive.md) 时执行的。

3.  如果驱动程序包的共同安装程序提供了 " [完成-安装" 操作](finish-install-actions--windows-vista-and-later-.md)，则共同安装程序将在分发介质上启动设备安装应用程序以安装特定于设备的应用程序。

**注意**  由于在启动设备安装应用程序之前已安装了 [驱动程序包](driver-packages.md) ，因此应用程序必须检测是否已安装驱动程序，并且仅安装设备特定的应用程序。

 

有关共同安装程序的详细信息，请参阅 [编写共同安装程序](writing-a-co-installer.md)。

有关通过共同安装程序启动设备安装应用程序的详细信息，请参阅 [通过共同安装程序启动设备安装应用程序的指南](guidelines-for-starting-device-installation-applications-through-co-in.md)。

 

 





