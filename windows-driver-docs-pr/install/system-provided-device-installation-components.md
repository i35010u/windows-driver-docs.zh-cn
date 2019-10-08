---
title: 系统提供的设备安装组件
description: 系统提供的设备安装组件
ms.assetid: faf586b9-ab99-4fee-a0d1-923000000189
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: a736de631067e947e9c47ef6cf9b3400a2a125c8
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007594"
---
# <a name="system-provided-device-installation-components"></a>系统提供的设备安装组件


以下列表描述了 Windows 操作系统所提供的设备安装组件：

<a href="" id="plug-and-play--pnp--manager"></a>即插即用（PnP）管理器  
即插即用（PnP）管理器为 Windows 中的 PnP 功能提供以下支持：

-   系统启动时的设备检测和枚举
-   在系统运行时添加或删除设备

有关详细信息，请参阅[PnP Manager](pnp-manager.md)。

<a href="" id="setupapi"></a>Setupapi.log  
安装程序应用程序编程接口（*setupapi.log*）包括常规设置功能（**安装程序 * **xxx*）和设备安装功能（** SetupDi * **xxx*和 **Di * ** * * * * *）。 这些函数可执行许多设备安装任务，如搜索 INF 文件、构建设备驱动程序的潜在列表、复制驱动程序文件、将信息写入注册表，以及注册设备共同安装程序。 大多数其他设备安装组件都调用这些功能。

有关详细信息，请参阅[setupapi.log](setupapi.md)。

<a href="" id="configuration-manager-api"></a>Configuration Manager API  
PnP 配置管理器 API 提供 Setupapi.log 未提供的基本安装和配置操作。 PnP 配置管理器功能执行低级别的任务，例如获取设备节点的状态（*devnode*）和管理资源描述符。 这些函数主要由 Setupapi.log 调用，但也可由其他设备安装组件调用。

<a href="" id="driver-store"></a>驱动程序存储  
从 Windows Vista 开始，驱动程序存储区是一组受信任的内置驱动程序包和第三方[驱动程序包](driver-packages.md)。 操作系统将此集合保留在本地硬盘上的安全位置。 对于设备，只能安装驱动程序存储区中的驱动程序包。

有关详细信息，请参阅[驱动程序存储](driver-store.md)。

<a href="" id="device-manager"></a>设备管理器  
使用设备管理器，你可以查看和管理系统上的设备。 例如，你可以查看设备状态并设置设备属性。

有关详细信息，请参阅[使用设备管理器](using-device-manager.md)。 另请参阅设备管理器中的帮助文档。

 

 





