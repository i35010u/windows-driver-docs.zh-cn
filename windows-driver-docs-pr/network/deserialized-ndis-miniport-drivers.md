---
title: 反序列化的 NDIS 微型端口驱动程序
description: 反序列化的 NDIS 微型端口驱动程序
ms.assetid: d133370a-48f4-425b-a2bd-d95ec8b5c369
keywords:
- 微型端口驱动程序 WDK 网络类型
- NDIS 微型端口驱动程序 WDK，类型
- 反序列化的 NDIS 微型端口驱动程序 WDK 网络
ms.date: 01/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: f9c3cf06239430cbb30659b38ffcf3202913a673
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381433"
---
# <a name="deserialized-ndis-miniport-drivers"></a>反序列化的 NDIS 微型端口驱动程序





所有 NDIS 6.0 和更高版本的驱动程序都都*反序列化*。

一个*反序列化的 NDIS 微型端口驱动程序*序列化的操作*MiniportXxx*函数和队列在内部的所有发送请求而不是依赖于 NDIS 来执行这些功能。 因此，反序列化的微型端口驱动程序可以实现全双工性能明显优于序列化的微型端口驱动程序。

反序列化的驱动程序模型是 NDIS 微型端口驱动程序的默认模型。 面向连接的微型端口驱动程序，以及使用 WDM 的下边缘，微型端口驱动程序必须反序列化的驱动程序。 在编写新的 NDIS 微型端口驱动程序时，您应编写反序列化的驱动程序。 如果可能，你还应端口旧驱动程序到 NDIS 6.0 或更高版本。 有关迁移的驱动程序的详细信息，请参阅：

-   [移植到 NDIS 6.0 的 NDIS 5.x 驱动程序](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)
-   [移植到 NDIS 6.20 NDIS 6.x 驱动程序](porting-ndis-6-x-drivers-to-ndis-6-20.md)
-   [移植到 NDIS 6.30 NDIS 6.x 驱动程序](porting-ndis-6-x-drivers-to-ndis-6-30.md)

它使用 NDIS 接口时，反序列化的微型端口驱动程序必须满足以下要求：

-   反序列化的微型端口驱动程序必须将自身标识这种情况下为 NDIS 在初始化过程。

-   反序列化的微型端口驱动程序必须以异步方式完成所有发送请求。 若要完成发送请求，无连接的 NDIS 6.0 和更高版本的微型端口驱动程序调用**NdisMSendNetBufferListsComplete**函数。 面向连接的 NDIS 6.0 和更高版本的微型端口驱动程序调用**NdisMCoSendNetBufferListsComplete**函数。

-   支持 NDIS 6.0 或更高版本的设置的反序列化的微型端口驱动程序**状态**NET 成员\_缓冲区\_列表结构，它将传递给**NdisMSendNetBufferListsComplete**.

-   如果反序列化的微型端口驱动程序不能立即完成发送请求，它不能用于排队到 NDIS 返回请求。 相反，微型端口驱动程序必须发送请求内部排队直到有足够的资源可用来传输数据。

-   反序列化的微型端口驱动程序必须检查传递到 NDIS 的结构在收到指示直到 NDIS 返回它们之后。 NDIS 返回 NET\_缓冲区\_微型端口驱动程序的列表结构*MiniportReturnNetBufferLists*函数。

反序列化的微型端口驱动程序必须满足以下驱动程序内部的要求：

-   反序列化的微型端口驱动程序必须保护其网络缓冲区队列[旋转锁](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-spin-locks)。 反序列化的微型端口驱动程序还必须保护其共享的状态同时访问由其自身*MiniportXxx*函数。

-   反序列化的微型端口驱动程序*MiniportXxx*函数可以运行在 IRQL &lt;= 调度\_级别。 因此，驱动程序编写器不能假定*MiniportXxx*将处理请求的顺序调用函数。 一个*MiniportXxx*函数可以抢占另*MiniportXxx*在较低的 IRQL 运行的函数。

-   反序列化的微型端口驱动程序负责网络缓冲区队列管理。 当微型端口驱动程序遇到资源问题时，它不能返回为排队到 NDIS 发送请求。 相反，微型端口驱动程序必须排队在内部的所有发送请求，直到有足够的资源是可用于将数据发送。

-   反序列化的微型端口驱动程序应完成发送请求以确定协议的顺序。

有关详细信息大约发送和接收的 NDIS 驱动程序的要求，请参阅[发送和接收操作](send-and-receive-operations.md)。

请注意，通常可完成反序列化的微型端口驱动程序将请求发送协议确定顺序。 但是，支持数据包优先级 (例如，IEEE 802.1 p) 的微型端口驱动程序可以对基于优先级的信息的发送请求重新排序。

 

 





