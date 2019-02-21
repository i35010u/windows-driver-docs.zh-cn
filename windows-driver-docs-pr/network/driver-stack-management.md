---
title: 驱动程序堆栈管理
description: 驱动程序堆栈管理
ms.assetid: 61d17e92-a1bf-42d9-b241-400b43b0ec0a
keywords:
- 驱动程序堆栈 WDK 连接网络、 管理
- 微型端口适配器 WDK 网络驱动程序堆栈
- 微型端口驱动程序 WDK 网络，微型端口适配器
- NDIS 微型端口驱动程序 WDK，微型端口适配器
- 协议绑定 WDK 网络
- 协议驱动程序 WDK net
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49fe5bd1e91088a1f61d86930d0c426f58dac966
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543927"
---
# <a name="driver-stack-management"></a>驱动程序堆栈管理





NDIS 6.0 引入了暂停和重新启动驱动程序堆栈的功能。 若要支持 NDIS 6.0 提供了 stack 管理功能，则必须重写旧驱动程序。

NDIS 6.0 还引入了 NDIS 筛选器驱动程序。 筛选器驱动程序可以监视和修改协议驱动程序和微型端口驱动程序之间的交互。 筛选器驱动程序是更轻松地实现并具有更少的处理开销比 NDIS 5。*x*中间驱动程序。 出于这些原因，应使用筛选器驱动程序，而不是筛选器中间驱动程序。

驱动程序堆栈包含以下逻辑元素：

<a href="" id="miniport-adapter"></a>微型端口适配器  
一个*微型端口适配器*是 NDIS 微型端口驱动程序或中间驱动程序的适配器实例。 中间的驱动程序的虚拟微型端口是微型端口适配器。 设备变得可用之后，NDIS 微型端口适配器上配置驱动程序堆栈的其他的元素。

<a href="" id="protocol-binding"></a>协议绑定  
一个*协议绑定*是协议驱动程序的绑定实例。 协议绑定绑定到微型端口适配器的 NDIS 协议驱动程序。 多个协议驱动程序可以绑定到的微型端口适配器。

<a href="" id="filter-module"></a>筛选器模块  
一个*筛选器模块*是筛选器驱动程序的实例。 NDIS 可以暂停驱动程序堆栈以插入、 删除或重新配置筛选器模块。 过滤器模块可以监视和修改的微型端口适配器的行为。

以下主题提供有关驱动程序堆栈、 驱动程序状态和驱动程序堆栈操作的详细信息：

-   [NDIS 驱动程序堆栈](ndis-driver-stack.md)
-   [适配器状态的微型端口驱动程序](adapter-states-of-a-miniport-driver.md)
-   [绑定协议驱动程序的状态](binding-states-of-a-protocol-driver.md)
-   [筛选器驱动程序的模块状态](module-states-of-a-filter-driver.md)
-   [NDIS 堆栈操作](ndis-stack-operations.md)

## <a name="related-topics"></a>相关主题


[NDIS 筛选器驱动程序](ndis-filter-drivers.md)

[中间的 NDIS 驱动程序](ndis-intermediate-drivers.md)

 

 






