---
title: 驱动程序包中包含的设备安装应用程序
description: 包含在驱动程序包中的设备安装应用程序
ms.assetid: bd6e182c-6b7a-4cde-bcc7-637ae6bf39be
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee2c252bc26494ff4542f1939bc7b211dcd0a2e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357953"
---
# <a name="device-installation-application-that-is-included-in-the-driver-package"></a>包含在驱动程序包中的设备安装应用程序


此方法描述通过其中一种方法共同安装程序，使用完成安装操作来安装特定于设备的应用程序。

在这种方法，设备安装应用程序和关联的安装文件属于[驱动程序包](driver-packages.md)，和驱动程序包的 INF 文件用于将应用程序和安装文件复制到驱动程序存储区。 因此，应用程序和驱动程序都安装在所有方案。

此方法具有以下优点：

-   如果共同安装程序提供[完成安装操作](finish-install-actions--windows-vista-and-later-.md)，可以使用此方法来安装驱动程序包，包括特定于设备的应用程序，在 Windows Vista 和更高版本的 Windows 上。

-   由于设备安装应用程序、 关联的安装文件和驱动程序都是相同的驱动程序包的一部分，它们将安装或在同一时间更新。 这会同步版本的驱动程序包中的所有组件。

但是，此方法还具有以下缺点：

-   如果它是的一部分，设备安装应用程序和关联的安装文件必须进行数字签名[驱动程序包](driver-packages.md)。 有关数字签名的详细信息，请参阅[驱动程序签名](driver-signing.md)。

    此外，驱动程序、 设备安装程序应用程序和关联的安装文件，必须提交到 Windows 硬件质量实验室 (WHQL) 作为单个驱动程序包时修改这些组件。 有关此过程的详细信息，请参阅[WHQL 版本签名](whql-release-signature.md)。

-   设备安装应用程序和关联的安装文件复制到用户的硬盘上的两个位置： 驱动程序存储区，以及 INF 文件中指定的目录[ **INF DestinationDirs 部分**](inf-destinationdirs-section.md).

-   可选特定于设备的应用程序在未安装通过设备安装应用程序，不能从分发介质安装或从 Internet 下载。

    因为设备安装应用程序和关联的安装文件进行签名的一部分[驱动程序包](driver-packages.md)，以确保允许仅通过设备安装应用程序安装的应用程序驱动程序包的完整性。

如果使用此方法，将进行以下操作每次用户插入分发介质之前安装该设备或 Windows 更新检测到设备的新驱动程序：

1.  如中所述安装设备驱动程序包[硬件第一个安装](hardware-first-installation.md)。

2.  [驱动程序包的](driver-packages.md)INF 文件将设备安装应用程序和关联的安装文件复制到用户的硬盘上，这通常是 Program Files 目录的目录。 这是在处理的一部分[ **INF CopyFiles 指令**](inf-copyfiles-directive.md) INF 文件中。

3.  如果驱动程序包的共同安装程序提供[完成安装操作](finish-install-actions--windows-vista-and-later-.md)，共同安装程序分发介质安装特定于设备的应用程序上启动的设备安装应用程序。

**请注意**  由于[驱动程序包](driver-packages.md)已安装的设备安装应用程序在启动之前，应用程序必须检测驱动程序已安装，并仅安装特定于设备的应用程序。

 

有关共同安装程序的详细信息，请参阅[编写共同安装程序](writing-a-co-installer.md)。

有关启动通过共同安装程序的设备安装应用程序的详细信息，请参阅[共同安装程序通过启动设备安装的应用程序指南](guidelines-for-starting-device-installation-applications-through-co-in.md)。

 

 





