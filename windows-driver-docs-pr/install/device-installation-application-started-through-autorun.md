---
title: 通过 AutoRun 启动的设备安装应用程序
description: 通过 AutoRun 启动的设备安装应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54ae786560086464a773ab7d29f6067e95b0de11
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782869"
---
# <a name="device-installation-application-started-through-autorun"></a>通过 AutoRun 启动的设备安装应用程序


此方法基于现有 [的软件优先安装](software-first-installation.md) 方法，以创建 [硬件优先安装](hardware-first-installation.md) 方案。 此方法依赖于 Windows Vista 和更高版本的 Windows 中支持的 [**INF HardwareId 指令**](inf-hardwareid-directive.md)。

在此方法中，分发介质上的 *设备安装应用程序* 在处理自动运行 .inf 文件的过程中启动。 当用户插入设备时，"发现新硬件" 向导会分析此文件，并查找与正在安装的设备相匹配的 [**INF HardwareId 指令**](inf-hardwareid-directive.md) 。 如果向导找到匹配项，则会调用启用了自动运行的设备安装应用程序来安装 [驱动程序包](driver-packages.md) 和设备特定的应用程序。

此方法具有以下优点：

-   独立硬件供应商 (Ihv) 可以通过将一个或多个 [**INF HardwareId 指令**](inf-hardwareid-directive.md) 添加到自动运行 .inf 文件，轻松地将此方法用于现有的自动运行兼容分发介质。 有关和自动运行和启用自动激活的应用程序的详细信息，请参阅 [创建 AutoRun-Enabled 应用程序](https://go.microsoft.com/fwlink/p/?linkid=133162)。

-   只有 [驱动程序包](driver-packages.md) 才能进行数字签名。 设备安装应用程序和关联的安装文件无需进行数字签名。 有关数字签名的详细信息，请参阅 [驱动程序签名](driver-signing.md)。

-   仅将驱动程序包复制到 [驱动程序存储区](driver-store.md)。 设备特定的应用程序安装在用户硬盘上的其他位置。

-   可以在驱动程序包更新过程中提示用户更新设备特定的应用程序。 此操作通过包的共同安装程序提供的 " [完成安装" 操作](finish-install-actions--windows-vista-and-later-.md) 进行。 通过这种方式，可以同步对驱动程序包和设备特定应用程序的更新。 另外，还可以从 Internet 下载其他或可选的应用程序，这些应用程序不在分发介质上。

但是，此方法也具有以下缺点：

-   此方法只能用于在 Windows Vista 和更高版本的 Windows 上安装 [驱动程序包](driver-packages.md) 和设备特定的应用程序安装。

-   分发媒体必须与自动兼容，如 CD 或 DVD。 [**INF HardwareId 指令**](inf-hardwareid-directive.md)不提供从 Internet 下载应用程序安装程序的任何功能。

 

 





