---
title: 筛选器驱动程序的特征
description: 筛选器驱动程序的特征
keywords:
- 筛选器驱动程序 WDK 网络，特征
- NDIS 筛选器驱动程序 WDK，特征
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abecd5ae621c0a887d5da513e7a4b04965b9e194
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838569"
---
# <a name="filter-driver-characteristics"></a>筛选器驱动程序的特征





筛选器驱动程序具有以下特征：

-   筛选器驱动程序的实例称为 *筛选器模块*。 筛选器模块附加到基础微型端口适配器。 来自同一筛选器驱动程序或不同筛选器驱动程序的多个筛选器模块可以通过适配器进行堆叠。

-   当在此类驱动程序和基础微型端口驱动程序之间安装筛选器模块时，不需要拥有过量协议驱动程序来提供备用功能 (否则，筛选器模块对过量协议驱动程序) 透明。

-   由于筛选器驱动程序不实现诸如中间驱动程序之类的虚拟微型端口，因此筛选器驱动程序不与设备对象相关联。 带有过量筛选器模块的微型端口适配器充当小型小型端口适配器的修改版本。 有关驱动程序堆栈的详细信息，请参阅 [NDIS 6.0 驱动程序堆栈](ndis-driver-stack.md)。

-   NDIS 使用配置信息按正确的驱动程序堆栈顺序将筛选器模块附加到适配器。 有关筛选器模块的驱动程序堆栈顺序的详细信息，请参阅 [筛选器驱动程序的 INF 文件设置](inf-file-settings-for-filter-drivers.md)。

-   NDIS 可以在驱动程序堆栈中动态插入或删除筛选器模块，或重新配置筛选器模块，而无需分解整个堆栈。 有关详细信息，请参阅 [修改正在运行的驱动程序堆栈](modifying-a-running-driver-stack.md)。

-   当 NDIS 重启驱动程序堆栈时，协议驱动程序可以在驱动程序堆栈中获取筛选器模块的列表。

    有关筛选器模块列表的详细信息，请参阅 [**NDIS \_ 协议 \_ 重新启动 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_restart_parameters)。

-   筛选器驱动程序可以筛选与基础微型端口适配器之间的大多数通信。 筛选器模块不与过量协议驱动程序和微型端口适配器之间的任何特定绑定相关联。 有关筛选器驱动程序可以提供的筛选服务类型的详细信息，请参阅 [筛选器驱动程序服务](filter-driver-services.md)。

-   筛选器驱动程序可以选择已筛选的服务，并且对于未筛选的服务可以跳过它们。 将绕过对所选服务的选择，并且可以动态地重新配置筛选的服务。 有关详细信息，请参阅 [Data 旁路 Mode](data-bypass-mode.md)。

-   NDIS 保证上下文空间的可用性 (参阅) 用于筛选器驱动程序的 [网络 \_ 缓冲区 \_ 列表 \_ 上下文结构](net-buffer-list-context-structure.md) 。 因此，筛选器驱动程序不需要包括代码来复制缓冲区以获取上下文空间。 有关如何管理缓冲区的详细信息，请参阅 [筛选器驱动程序缓冲区管理](filter-driver-buffer-management.md)。

 

