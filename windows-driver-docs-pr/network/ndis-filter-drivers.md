---
title: 筛选器驱动程序
description: 筛选器驱动程序
ms.assetid: 626547ba-4c26-4be7-b209-c5e26daf56ab
keywords:
- 筛选器驱动程序 WDK 网络体系结构
- NDIS 筛选器驱动程序 WDK，体系结构
- 筛选器模块 WDK 网络
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 234b673508213d2fdee0be7bc929bcd5c12564de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385520"
---
# <a name="filter-drivers"></a>筛选器驱动程序

NDIS 6.0 引入了 NDIS 筛选器驱动程序。 筛选器驱动程序可以监视和修改协议驱动程序和微型端口驱动程序之间的交互。 筛选器驱动程序是更轻松地实现并具有更少的处理开销比 NDIS 中间层驱动程序。

一个*筛选器模块*是筛选器驱动程序的实例。 下图所示，筛选器模块通常分为几级之间微型端口适配器和协议绑定。

![说明与筛选器模块的 ndis 驱动程序堆栈的关系图](images/filterstack.png)

使用 NDIS 和其他 NDIS 驱动程序在 NDIS 库中，筛选器驱动程序进行通信。 NDIS 库导出一套完整的函数 (**NdisF * Xxx*** 和其他**Ndis * Xxx*** 函数)，它封装的所有筛选器驱动程序必须调用操作系统函数。 筛选器驱动程序，反过来，必须导出一组的入口点 (*FilterXxx*函数) 的 NDIS 调用其自身的用途，或代表其他驱动程序，访问筛选器驱动程序。

> [!NOTE]
> 有关 NDIS 驱动程序堆栈和一个显示所有四个的 NDIS 驱动程序类型之间的关系图的详细信息，请参阅[NDIS 驱动程序堆栈](ndis-driver-stack.md)。

## <a name="related-topics"></a>相关主题

[NDIS 筛选器驱动程序](ndis-filter-drivers2.md)

[NDIS 筛选器驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)