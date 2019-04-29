---
title: 通过 AutoRun 启动的设备安装应用程序
description: 通过 AutoRun 启动的设备安装应用程序
ms.assetid: 9b520d82-2293-4936-99fe-30bf6753ba9f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79431a2febc178fe9d8e59c135adfa01f4cdc464
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357864"
---
# <a name="device-installation-application-started-through-autorun"></a>通过 AutoRun 启动的设备安装应用程序


此方法基于现有[软件的第一个安装](software-first-installation.md)方法来创建[硬件第一个安装](hardware-first-installation.md)方案。 此方法依赖于[ **INF HardwareId 指令**](inf-hardwareid-directive.md)，这 Windows Vista 和更高版本的 Windows 中受支持。

在此方法中，*设备安装应用程序*在分布区中启动的 Autorun.inf 文件处理的一部分。 当用户插入设备时，发现新硬件向导分析此文件中，并寻找[ **INF HardwareId 指令**](inf-hardwareid-directive.md)的匹配正在安装的设备。 如果向导找到匹配项，它将调用启用了自动运行的设备安装应用程序来安装[驱动程序包](driver-packages.md)和特定于设备的应用程序。

此方法具有以下优点：

-   独立硬件供应商 (Ihv) 可以轻松地使用一个或多个现有自动运行兼容分发介质通过添加此方法[ **INF HardwareId 指令**](inf-hardwareid-directive.md) Autorun.inf 文件。 有关详细信息和自动运行和启用自动运行的应用程序，请参阅[创建 AutoRun-Enabled 应用程序](https://go.microsoft.com/fwlink/p/?linkid=133162)。

-   仅[驱动程序包](driver-packages.md)必须进行数字签名。 设备安装应用程序和关联的安装文件无需进行数字签名。 有关数字签名的详细信息，请参阅[驱动程序签名](driver-signing.md)。

-   仅将驱动程序包复制到[驱动程序存储区](driver-store.md)。 特定于设备的应用程序被安装在用户的硬盘上的其他位置。

-   可以在驱动程序包更新期间提示用户，若要更新的特定于设备的应用程序。 通过将发生这种情况[完成安装操作](finish-install-actions--windows-vista-and-later-.md)提供的包的辅助安装程序。 这样一来，可以同步到驱动程序包和特定于设备的应用程序的更新。 此外，附加或可选应用程序，这不是分发介质上，可以从 Internet 下载。

但是，此方法还具有以下缺点：

-   此方法可用于安装[驱动程序包](driver-packages.md)和仅在 Windows Vista 和更高版本的 Windows 上的特定于设备的应用程序安装。

-   在分发媒体必须自动运行兼容，如 CD 或 DVD。 [ **INF HardwareId 指令**](inf-hardwareid-directive.md)不提供任何功能从 Internet 下载应用程序安装程序。

 

 





