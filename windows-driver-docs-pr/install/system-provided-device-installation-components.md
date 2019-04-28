---
title: 系统提供的设备安装组件
description: 系统提供的设备安装组件
ms.assetid: faf586b9-ab99-4fee-a0d1-923000000189
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab257f2c828a30e599c7b951148b986c1e05fe75
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339649"
---
# <a name="system-provided-device-installation-components"></a>系统提供的设备安装组件


以下列表介绍了由 Windows 操作系统提供的设备安装组件：

<a href="" id="plug-and-play--pnp--manager"></a>插即用 (PnP) 管理器  
插即用 (PnP) 管理器对于 Windows 中的即插即用功能提供以下支持：

-   设备检测和枚举期间启动系统
-   添加或删除设备，系统运行时

有关详细信息，请参阅[PnP 管理器](pnp-manager.md)。

<a href="" id="setupapi"></a>SetupAPI  
安装程序应用程序编程接口 (*SetupAPI*) 包括常规设置函数 (**安装 * **Xxx*) 和设备安装函数 (** SetupDi * **Xxx*和 **Di * * * Xxx*)。 这些函数执行很多的设备安装任务，例如，搜索 INF 文件、 生成一系列潜在的设备驱动程序、 驱动程序文件复制、 将信息写入到注册表中，和注册设备共同安装程序。 大多数其他设备安装组件调用这些函数。

有关详细信息，请参阅[SetupAPI](setupapi.md)。

<a href="" id="configuration-manager-api"></a>配置管理器 API  
即插即用的配置管理器 API 提供了基本安装和配置操作不由安装程序 Api 提供的。 即插即用的配置管理器函数执行低级任务，例如获取设备节点的状态 (*devnode*) 和管理资源描述符。 这些函数主要由安装程序 Api 调用，但也可以调用其他设备安装组件。

<a href="" id="driver-store"></a>驱动程序存储区  
从 Windows Vista 开始，驱动程序存储区是受信任的框中和第三方集合[驱动程序包](driver-packages.md)。 操作系统维护此集合中在本地硬盘上的安全位置。 可以为设备安装的驱动程序包将驱动程序存储区中。

有关详细信息，请参阅[驱动程序存储区](driver-store.md)。

<a href="" id="device-manager"></a>设备管理器  
使用设备管理器中，可以查看和管理的系统上的设备。 例如，您可以查看设备状态和设置设备属性。

有关详细信息，请参阅[使用设备管理器](using-device-manager.md)。 此外，请参阅帮助文档在设备管理器。

 

 





