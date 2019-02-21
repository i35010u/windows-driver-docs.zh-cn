---
title: 筛选器模块发送和接收操作
description: 筛选器模块发送和接收操作
ms.assetid: 208f9af6-cde4-4801-9355-daa6633d7d0b
keywords:
- 筛选器模块 WDK 网络中，发送操作
- 筛选器模块 WDK 网络中，接收操作
- 筛选器驱动程序 WDK 网络中，发送操作
- NDIS 筛选器驱动程序 WDK 中，发送操作
- 筛选器驱动程序 WDK 网络中，接收操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dfb8e01286a1388539682859872f290d97ed16d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546915"
---
# <a name="filter-module-send-and-receive-operations"></a>筛选器模块发送和接收操作





本部分记录发送和接收操作的 NDIS 6.0 筛选器驱动程序。 筛选器驱动程序可以启动的发送请求并接收指示或筛选的请求和其他驱动程序的迹象。

筛选器模块是堆积微型端口适配器上。 有关驱动程序堆栈的详细信息，请参阅[NDIS 6.0 驱动程序堆栈](ndis-driver-stack.md)。

驱动程序堆栈中的筛选器模块可以筛选所有发送请求并接收与基础适配器相关联的迹象。 这适用于所有协议绑定到适配器。 详细了解 NDIS 6.0 发送和接收操作，请参阅[发送和接收操作](send-and-receive-operations.md)。

筛选器驱动程序不提供直接支持为旧的发送和接收操作上，基于[ **NDIS\_数据包**](https://msdn.microsoft.com/library/windows/hardware/ff557086)结构。 相反，NDIS 将从旧的微型端口驱动程序收到指示[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构。 此外，NDIS 处理从基于 NET 的发送请求所需的转换\_到旧的缓冲区结构发送请求基于 NDIS\_数据包结构。

**请注意**  筛选器驱动程序可以更改发送和接收*FliterXxx*动态函数的筛选器模块。 有关详细信息，请参阅[数据绕过模式](data-bypass-mode.md)。

 

以下主题提供其他信息筛选器驱动程序发送和接收操作：

[筛选驱动程序缓冲区管理](filter-driver-buffer-management.md)

[从筛选器驱动程序发送数据](sending-data-from-a-filter-driver.md)

[正在取消筛选器驱动程序中的发送请求](canceling-a-send-request-in-a-filter-driver.md)

[在筛选器驱动程序中接收数据](receiving-data-in-a-filter-driver.md)

 

 





