---
title: 软件优先安装
description: 软件优先安装
ms.assetid: 2199316d-17d5-463a-8c97-f89c87473f20
keywords:
- 安装应用程序 WDK，第一个软件的安装
- 设备安装应用程序 WDK，第一个软件的安装
- 分发中等 WDK 设备安装，第一个软件的安装
- 软件的第一个安装 WDK 设备安装
- 启用了自动运行的安装应用程序 WDK
- 设备安装 WDK，类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e86fabffcf0e12708ee9936c2752a9ebf37356c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348599"
---
# <a name="software-first-installation"></a>软件优先安装


第一个软件的安装涉及到过渡环境和预安装的应用[驱动程序包](driver-packages.md)之前硬件系统上在插入设备。 在插入设备后，安装驱动程序包从驱动程序。

如果用户插入设备之前插入分发介质，可以启用自动运行的安装应用程序：

-   [检查正在进行中安装](checking-for-in-progress-installations.md)，并停止执行其他安装活动是否正在进行中。

-   [确定是否在插入设备](determining-whether-a-device-is-plugged-in.md)。

-   [预安装的驱动程序包](preinstalling-driver-packages.md)

-   使用 Microsoft 安装程序[安装特定于设备的应用程序](installing-device-specific-applications.md)。

-   如果该设备是"热插拔"，告诉用户来插入该类。

    如果在总线不提供热即插即用通知，通过调用启动重新列举[ **CM_Reenumerate_DevNode**](https://msdn.microsoft.com/library/windows/hardware/ff539763)。

-   如果设备不是热插拔，告知用户关闭系统、 插入设备，并重新启动系统。

 

 





