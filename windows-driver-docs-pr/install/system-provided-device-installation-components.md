---
title: 系统提供的设备安装组件
description: 系统提供的设备安装组件
ms.assetid: faf586b9-ab99-4fee-a0d1-923000000189
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 21572205ffc743caa2a05cad9f9f97903bcbd1e9
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "72512074"
---
# <a name="system-provided-device-installation-components"></a>系统提供的设备安装组件


以下列表描述了 Windows 操作系统所提供的设备安装组件：

<a href="" id="plug-and-play--pnp--manager"></a>即插即用 (PnP) 管理器  
即插即用 (PnP) 管理器为 Windows 中的 PnP 功能提供以下支持：

-   系统启动时的设备检测和枚举
-   在系统运行时添加或删除设备

有关详细信息，请参阅 [PnP 管理器](pnp-manager.md)。

<a href="" id="setupapi"></a>SetupAPI  
安装程序应用程序编程接口 (*SetupAPI*) 包含常规安装函数 (**Setup***Xxx*) 和设备安装函数（** SetupDi***Xxx* 和 **Di***Xxx*）。 这些函数执行许多设备安装任务，如搜索 INF 文件、构建设备驱动程序的潜在列表、复制驱动程序文件、将信息写入注册表，以及注册设备共同安装程序。 大多数其他设备安装组件都调用这些函数。

有关详细信息，请参阅 [SetupAPI ](setupapi.md)。

<a href="" id="configuration-manager-api"></a>配置管理器 API  
PnP 配置管理器 API 提供 SetupAPI 未提供的基本安装和配置操作。 PnP 配置管理器函数执行低级别的任务，例如获取设备节点的状态 (*devnode*) 和管理资源描述符。 这些函数主要由 SetupAPI 调用，但也可由其他设备安装组件调用。

<a href="" id="driver-store"></a>驱动程序存储  
驱动程序存储是内置驱动程序包和第三方[驱动程序包](driver-packages.md)的受信任集合。 操作系统将此集合保留在本地硬盘上的安全位置。 对于设备，只能安装驱动程序存储中的驱动程序包。

有关详细信息，请参阅[驱动程序存储](driver-store.md)。

<a href="" id="device-manager"></a>设备管理器  
使用设备管理器，可以查看和管理系统上的设备。 例如，可以查看设备状态并设置设备属性。

有关详细信息，请参阅[使用设备管理器](using-device-manager.md)。 另请参阅设备管理器中的帮助文档。

 

 





