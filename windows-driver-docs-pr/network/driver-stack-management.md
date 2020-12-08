---
title: 驱动程序堆栈管理
description: 驱动程序堆栈管理
keywords:
- 驱动程序堆栈 WDK 网络，管理
- 微型端口适配器 WDK 网络，驱动程序堆栈
- 微型端口驱动程序 WDK 网络，微型端口适配器
- NDIS 微型端口驱动程序 WDK、微型端口适配器
- 协议绑定 WDK 网络
- 协议驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fbe2cd8fc75d43b43bf360cab8eee1fdb087a3a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808627"
---
# <a name="driver-stack-management"></a>驱动程序堆栈管理





NDIS 6.0 引入了暂停和重新启动驱动程序堆栈的功能。 若要支持 NDIS 6.0 提供的堆栈管理功能，必须重写旧驱动程序。

NDIS 6.0 还引入了 NDIS 筛选器驱动程序。 筛选器驱动程序可以监视和修改协议驱动程序和微型端口驱动程序之间的交互。 筛选器驱动程序的实现更加简单，处理开销比 NDIS 5 更少。*x* 中间驱动程序。 出于这些原因，应该使用筛选器驱动程序，而不是筛选中间驱动程序。

驱动程序堆栈包含以下逻辑元素：

<a href="" id="miniport-adapter"></a>微型端口适配器  
*微型端口适配器* 是 NDIS 微型端口驱动程序或中间驱动程序的适配器实例。 中间驱动程序的虚拟小型端口是一个微型端口适配器。 在设备可用之后，NDIS 会通过微型端口适配器配置驱动程序堆栈的其他元素。

<a href="" id="protocol-binding"></a>协议绑定  
*协议绑定* 是协议驱动程序的绑定实例。 协议绑定将 NDIS 协议驱动程序绑定到微型端口适配器。 多个协议驱动程序可以绑定到微型端口适配器。

<a href="" id="filter-module"></a>筛选器模块  
*筛选器模块* 是筛选器驱动程序的实例。 NDIS 可以暂停驱动程序堆栈以插入、删除或重新配置筛选器模块。 筛选器模块可以监视和修改微型端口适配器的行为。

以下主题提供有关驱动程序堆栈、驱动程序状态和驱动程序堆栈操作的详细信息：

-   [NDIS 驱动程序堆栈](ndis-driver-stack.md)
-   [微型端口驱动程序的适配器状态](adapter-states-of-a-miniport-driver.md)
-   [协议驱动程序的绑定状态](binding-states-of-a-protocol-driver.md)
-   [筛选器驱动程序的模块状态](module-states-of-a-filter-driver.md)
-   [NDIS 堆栈操作](starting-a-driver-stack.md)

## <a name="related-topics"></a>相关主题


[NDIS 筛选器驱动程序](ndis-filter-drivers.md)

[NDIS 中间驱动程序](ndis-intermediate-drivers.md)

 

 






