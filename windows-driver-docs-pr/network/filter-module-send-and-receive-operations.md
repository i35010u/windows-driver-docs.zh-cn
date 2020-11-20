---
title: 筛选器模块发送和接收操作
description: 筛选器模块发送和接收操作
ms.assetid: 208f9af6-cde4-4801-9355-daa6633d7d0b
keywords:
- 筛选器模块 WDK 网络，发送操作
- 筛选器模块 WDK 网络，接收操作
- 筛选器驱动程序 WDK 网络，发送操作
- NDIS 筛选器驱动程序 WDK，发送操作
- 筛选器驱动程序 WDK 网络，接收操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4de512f62d439d888da32d82d895fb9a372f6019
ms.sourcegitcommit: 3da878e2fb4ce7d81bfa4177050a8c6c1a0544cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2020
ms.locfileid: "94983274"
---
# <a name="filter-module-send-and-receive-operations"></a>筛选器模块发送和接收操作





本部分记录了 NDIS 6.0 筛选器驱动程序的发送和接收操作。 筛选器驱动程序可以启动发送请求并接收指示，或者筛选其他驱动程序的请求和指示。

筛选器模块堆积在微型端口适配器上。 有关驱动程序堆栈的详细信息，请参阅 [NDIS 6.0 驱动程序堆栈](ndis-driver-stack.md)。

驱动程序堆栈中的筛选器模块可以筛选所有发送请求并接收与基础适配器关联的指示。 这适用于所有协议绑定到适配器的情况。 有关 NDIS 6.0 发送和接收操作的详细信息，请参阅 [发送和接收操作](send-and-receive-operations.md)。

筛选器驱动程序不提供对基于 [**NDIS \_ 数据包**](/previous-versions/windows/hardware/network/ff557086(v=vs.85)) 结构的传统发送和接收操作的直接支持。 取而代之的是，NDIS 会将来自旧微型端口驱动程序的接收指示转换为 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构。 此外，NDIS 还处理从将基于 NET BUFFER 结构的发送请求转换 \_ 为基于 NDIS 数据包结构的旧发送请求的所需转换 \_ 。

**注意**  筛选器驱动程序可以动态更改筛选器模块的 send 和 receive *FilterXxx* 函数。 有关详细信息，请参阅 [Data 旁路 Mode](data-bypass-mode.md)。

 

以下主题提供了有关筛选器驱动程序发送和接收操作的其他信息：

[筛选器驱动程序缓冲区管理](filter-driver-buffer-management.md)

[从筛选器驱动程序发送数据](sending-data-from-a-filter-driver.md)

[取消筛选器驱动程序中的发送请求](canceling-a-send-request-in-a-filter-driver.md)

[在筛选器驱动程序中接收数据](receiving-data-in-a-filter-driver.md)

 

