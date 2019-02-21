---
title: 筛选器驱动程序特征
description: 筛选器驱动程序特征
ms.assetid: 95e302c1-687e-4a30-b3bc-9d272c688cba
keywords:
- 筛选器驱动程序 WDK 网络特征
- NDIS 筛选器驱动程序 WDK，特征
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ca033e85a792987c76b134426d66f7172fb5fec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524774"
---
# <a name="filter-driver-characteristics"></a>筛选器驱动程序特征





筛选器驱动程序具有以下特征：

-   筛选器驱动程序的实例称为*筛选器模块*。 筛选器模块会附加到基础的微型端口适配器。 从同一个筛选器驱动程序或不同的筛选器驱动程序的多个筛选器模块可以通过适配器进行堆叠。

-   基础协议驱动程序不需要在筛选器模块均已安装此类驱动程序和基础微型端口驱动程序之间提供替代功能 （否则所述，筛选器模块是透明的过量协议驱动程序）。

-   由于筛选器驱动程序未实现中间驱动程序等的虚拟微型端口，筛选器驱动程序不是与设备对象相关联。 具有过量筛选器模块的微型端口适配器作为微型端口适配器的修改版本。 有关驱动程序堆栈的详细信息，请参阅[NDIS 6.0 驱动程序堆栈](ndis-driver-stack.md)。

-   NDIS 使用配置信息将附加到正确的驱动程序堆栈顺序中的适配器的筛选器模块。 有关筛选器模块的驱动程序堆栈顺序的详细信息，请参阅[筛选器驱动程序的 INF 文件设置](inf-file-settings-for-filter-drivers.md)。

-   NDIS 可以动态地插入或删除驱动程序堆栈中的筛选器模块或重新筛选器模块中，配置而无需关闭整个堆栈。 有关详细信息，请参阅[修改运行驱动程序堆栈](modifying-a-running-driver-stack.md)。

-   NDIS 重新启动驱动程序堆栈时，协议驱动程序可以获取驱动程序堆栈中的筛选器模块的列表。

    有关筛选器模块的列表的详细信息，请参阅[ **NDIS\_协议\_重新启动\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566844)。

-   筛选器驱动程序可以筛选基础的微型端口适配器的大多数通信。 筛选器模块不与任何基础协议驱动程序微型端口适配器之间的特定绑定相关联。 有关筛选的筛选器驱动程序可以提供服务的类型的详细信息，请参阅[筛选器驱动程序服务](filter-driver-services.md)。

-   筛选器驱动程序可以选择进行筛选，可以忽略有关未筛选的服务的服务。 选择会绕过的服务和服务进行筛选后的动态重新配置。 有关详细信息，请参阅[数据绕过模式](data-bypass-mode.md)。

-   NDIS 保证上下文空间的可用性 (请参阅[NET\_缓冲区\_列表\_上下文结构](net-buffer-list-context-structure.md)) 的筛选器驱动程序。 因此，不需要将该代码复制缓冲区获取上下文空间包括筛选器驱动程序。 有关如何管理缓冲区的详细信息，请参阅[筛选器驱动程序缓冲区管理](filter-driver-buffer-management.md)。

 

 





