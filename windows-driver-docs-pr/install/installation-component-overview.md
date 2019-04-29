---
title: 安装组件概述
description: 安装组件概述
ms.assetid: 29d14a3a-e89a-47ef-bd36-ee3cdcde2cd7
keywords:
- 驱动程序包 WDK、 安装组件
- WDK、 安装组件的包
- 驱动程序安装 WDK，所需的信息
- 操作系统 WDK，驱动程序安装信息
- 安装驱动程序 WDK，所需的信息
- 安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d72b0060c69fa6b7bd3df118b51699e727c31bcb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325813"
---
# <a name="installation-component-overview"></a>安装组件概述





[设备安装概述](overview-of-device-and-driver-installation.md)部分提供了详细信息，Microsoft Windows 操作系统如何找到并安装了设备和驱动程序，以及此类安装中所涉及的组件。

若要安装的设备或驱动程序，操作系统需要最低的以下信息：

-   每个设备或驱动程序支持的操作系统名称和版本数

-   设备的安装程序类 GUID 和安装程序类

-   驱动程序版本信息

-   以及其源和目标位置的驱动程序文件的名称

-   特定于设备的信息，包括[硬件 ID](hardware-ids.md)和[兼容 Id](compatible-ids.md)

-   名称[目录 (.cat) 文件](catalog-files.md)

-   了解如何以及何时加载的服务所提供的每个驱动程序 （Windows 2000 和更高版本的 Windows）

可以在设备 INF 文件中提供所有此类信息。 对于大多数设备和驱动程序组合，INF 文件是需要的仅安装组件。 所有设备和驱动程序都要求一个 INF 文件。 有关详细信息，请参阅[提供 INF 文件](supplying-an-inf-file.md)。

如果引导系统中涉及你的设备，则安装要求可能有所不同。 请参阅[安装启动驱动程序](installing-a-boot-start-driver.md)。

 

 





