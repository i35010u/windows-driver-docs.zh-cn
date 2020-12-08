---
title: 安装组件概述
description: 安装组件概述
keywords:
- 驱动程序包 WDK，安装组件
- 包 WDK，安装组件
- 驱动程序安装 WDK，所需信息
- 操作系统 WDK，驱动程序安装信息
- 安装驱动程序 WDK，所需信息
- 安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 020d235e6a672bd28504ac568d29e20cd3546e46
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805473"
---
# <a name="installation-component-overview"></a>安装组件概述





" [设备安装概述](overview-of-device-and-driver-installation.md) " 部分提供了有关 Microsoft Windows 操作系统如何查找和安装设备和驱动程序以及此类安装中所涉及组件的详细信息。

若要安装设备或驱动程序，操作系统至少需要以下信息：

-   支持该设备或驱动程序的每个操作系统的名称和版本号

-   设备的安装类 GUID 和安装类

-   驱动程序版本信息

-   驱动程序文件的名称及其源和目标位置

-   设备特定的信息，包括 [硬件 ID](hardware-ids.md) 和 [兼容 id](compatible-ids.md)

-   目录的名称 [ () 文件](catalog-files.md)

-   有关如何以及何时加载每个驱动程序提供的服务的信息 (Windows 2000 和更高版本的 Windows) 

可以在设备的 INF 文件中提供所有这些信息。 对于大多数设备和驱动程序组合，INF 文件是唯一需要的安装组件。 所有设备和驱动程序都需要一个 INF 文件。 有关详细信息，请参阅[提供 INF 文件](supplying-an-inf-file.md)。

如果设备正在启动系统，则安装要求会有所不同。 请参阅 [安装启动驱动程序](installing-a-boot-start-driver.md)。

 

 





