---
title: PnP 组件
description: PnP 组件
ms.assetid: 33612da4-1ddb-40cf-a8a2-838f85b52cd6
keywords:
- 即插即用 WDK 内核组件
- 即插即用和播放 WDK 内核组件
- WDK 即插即用的软件组件
- 即插即用驱动程序 WDK 内核
- 用户模式即插即用管理器 WDK
- 内核模式即插即用 manager WDK
- 即插即用经理 WDK
- 即插即用组件 WDK 用户模式
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b735f72b2ef964273e737486b67fd652e33e211
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369242"
---
# <a name="pnp-components"></a>PnP 组件





下图显示了协同工作来支持即插即用的组件。

![演示如何插软件组件的关系图](images/pnpcomp.png)

PnP 管理器有两个部分： 内核模式即插即用管理器和用户模式即插即用管理器。 内核模式即插即用管理器与操作系统组件和驱动程序来配置、 管理和维护设备进行交互。 与用户模式下安装组件，如类安装程序、 配置和安装的设备进行交互的用户模式即插即用管理器。 此外在与应用程序，例如，注册的设备更改通知的应用程序和设备事件发生时通知应用程序进行交互的用户模式即插即用管理器。

即插即用驱动程序支持的计算机上的物理、 逻辑和虚拟设备。 术语"即插即用驱动程序"是指任何 Windows 驱动程序，它支持在本部分中描述的接口。 虽然大多数即插即用驱动程序还 WDM 驱动程序，因此源兼容跨 Windows 平台，一些驱动程序支持 PnP 而无需完全实现 WDM。

所有驱动程序应支持即插即用和电源管理。 如果单个驱动程序不支持即插即用和电源管理，它作为一个整体约束系统的 PnP 和电源管理支持。

请参阅[设备安装概述](https://msdn.microsoft.com/library/windows/hardware/ff549455)有关设备和驱动程序安装程序的信息，包括 (INF) 文件、 CAT 文件和注册表。

 

 




