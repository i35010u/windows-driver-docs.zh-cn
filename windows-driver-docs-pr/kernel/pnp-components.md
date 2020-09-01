---
title: PnP 组件
description: PnP 组件
ms.assetid: 33612da4-1ddb-40cf-a8a2-838f85b52cd6
keywords:
- PnP WDK 内核，组件
- 即插即用 WDK 内核，组件
- 软件组件 WDK PnP
- PnP 驱动程序 WDK 内核
- 用户模式 PnP 管理器 WDK
- 内核模式 PnP 管理器 WDK
- PnP 管理器 WDK
- PnP 组件 WDK 用户模式
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0516b4c519d53a9a3a9657ee2e68914d07967c7f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191845"
---
# <a name="pnp-components"></a>PnP 组件





下图显示了协同工作以支持 PnP 的组件。

![说明即插即用软件组件的示意图](images/pnpcomp.png)

PnP 管理器有两部分：内核模式 PnP 管理器和用户模式 PnP 管理器。 内核模式 PnP 管理器与操作系统组件和驱动程序交互，以配置、管理和维护设备。 用户模式 PnP 管理器与用户模式安装组件（如类安装程序）进行交互，以配置和安装设备。 用户模式 PnP 管理器还与应用程序进行交互，例如，注册应用程序以通知设备更改，并在设备事件发生时通知应用程序。

PnP 驱动程序支持计算机上的物理设备、逻辑设备和虚拟设备。 术语 "PnP 驱动程序" 是指支持此部分中所述接口的任何 Windows 驱动程序。 尽管大多数 PnP 驱动程序也是 WDM 驱动程序，因而跨 Windows 平台提供源兼容性，但少数驱动程序支持 PnP，无需完全实现 WDM。

所有驱动程序都应支持 PnP 和电源管理。 如果单个驱动程序不支持 PnP 和电源管理，则它会限制系统的 PnP 和电源管理支持。

请参阅 [设备安装概述](../install/overview-of-device-and-driver-installation.md) ，了解有关设备和驱动程序设置的信息，包括 (INF) 文件、CAT 文件和注册表。

 

