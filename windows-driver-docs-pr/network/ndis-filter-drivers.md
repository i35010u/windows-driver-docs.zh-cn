---
title: 筛选器驱动程序
description: 筛选器驱动程序
ms.assetid: 626547ba-4c26-4be7-b209-c5e26daf56ab
keywords:
- 筛选器驱动程序 WDK 网络，体系结构
- NDIS 筛选器驱动程序 WDK，体系结构
- 筛选器模块 WDK 网络
ms.date: 11/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7109a28ea32251b2b978997c4ceaf1651472f83e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838896"
---
# <a name="filter-drivers"></a>筛选器驱动程序

NDIS 6.0 引入了 NDIS 筛选器驱动程序。 筛选器驱动程序可以监视和修改协议驱动程序和微型端口驱动程序之间的交互。 筛选器驱动程序的实现更加简单，处理开销比 NDIS 中间驱动程序更少。

*筛选器模块*是筛选器驱动程序的实例。 如下图所示，筛选器模块通常在微型端口适配器和协议绑定之间分层。

![阐释带有筛选器模块的 ndis 驱动程序堆栈的关系图](images/filterstack.png)

筛选器驱动程序通过 NDIS 库与 NDIS 和其他 NDIS 驱动程序通信。 NDIS 库导出一组完整的函数（**NdisF * xxx*** 和其他**NDIS * xxx*** 函数），该函数封装筛选器驱动程序必须调用的所有操作系统函数。 相反，筛选器驱动程序必须导出一组入口点（*FilterXxx*函数），这些入口点（一组入口点）用于 NDIS 调用自身的目的，或者代表其他驱动程序来访问筛选器驱动程序。

> [!NOTE]
> 有关 NDIS 驱动程序堆栈的详细信息以及显示所有四个 NDIS 驱动程序类型之间关系的关系图，请参阅[NDIS 驱动程序堆栈](ndis-driver-stack.md)。

## <a name="related-topics"></a>相关主题

[NDIS 筛选器驱动程序](ndis-filter-drivers2.md)

[NDIS 筛选器驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)