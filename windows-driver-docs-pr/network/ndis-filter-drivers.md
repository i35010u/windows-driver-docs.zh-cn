---
title: 筛选器驱动程序
description: 筛选器驱动程序
keywords:
- 筛选器驱动程序 WDK 网络，体系结构
- NDIS 筛选器驱动程序 WDK，体系结构
- 筛选器模块 WDK 网络
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 04557dcd610041977e2655c00ae9317eb7c515af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798033"
---
# <a name="filter-drivers"></a>筛选器驱动程序

NDIS 6.0 引入了 NDIS 筛选器驱动程序。 筛选器驱动程序可以监视和修改协议驱动程序和微型端口驱动程序之间的交互。 筛选器驱动程序的实现更加简单，处理开销比 NDIS 中间驱动程序更少。

*筛选器模块* 是筛选器驱动程序的实例。 如下图所示，筛选器模块通常在微型端口适配器和协议绑定之间分层。

![阐释带有筛选器模块的 ndis 驱动程序堆栈的关系图](images/filterstack.png)

筛选器驱动程序通过 NDIS 库与 NDIS 和其他 NDIS 驱动程序通信。 NDIS 库导出一组完整的函数 (**NdisF * xxx*** 和其他 **NDIS * xxx*** 函数) 封装筛选器驱动程序必须调用的所有操作系统函数。 相反，筛选器驱动程序必须导出 (*FilterXxx* 函数的一组入口点) 该函数由 NDIS 调用其自身用途，或代表其他驱动程序来访问筛选器驱动程序。

> [!NOTE]
> 有关 NDIS 驱动程序堆栈的详细信息以及显示所有四个 NDIS 驱动程序类型之间关系的关系图，请参阅 [NDIS 驱动程序堆栈](ndis-driver-stack.md)。

## <a name="related-topics"></a>相关主题

[NDIS 筛选器驱动程序](./roadmap-for-developing-ndis-filter-drivers.md)

[NDIS 筛选器驱动程序参考](/windows-hardware/drivers/ddi/_netvista/)
