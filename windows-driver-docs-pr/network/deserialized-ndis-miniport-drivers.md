---
title: 反序列化的 NDIS 微型端口驱动程序
description: 反序列化的 NDIS 微型端口驱动程序
ms.assetid: d133370a-48f4-425b-a2bd-d95ec8b5c369
keywords:
- 微型端口驱动程序 WDK 网络，类型
- NDIS 微型端口驱动程序 WDK，类型
- 反序列化 NDIS 微型端口驱动程序 WDK 网络
ms.date: 01/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: f78387c3f5847abe36a22fc9a479d81ea8f7f32b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218430"
---
# <a name="deserialized-ndis-miniport-drivers"></a>反序列化的 NDIS 微型端口驱动程序





所有 NDIS 6.0 和更高版本的驱动程序均已 *反序列化*。

*反序列化的 NDIS 微型端口驱动程序*序列化其自己的*MiniportXxx*函数的操作，并在内部发送请求，而不是依赖 NDIS 来执行这些功能。 因此，反序列化的微型端口驱动程序可以比序列化微型端口驱动程序实现明显更好的全双工性能。

反序列化的驱动程序模型是 NDIS 微型端口驱动程序的默认模型。 面向连接的微型端口驱动程序以及具有 WDM 下边缘的微型端口驱动程序必须是反序列化的驱动程序。 编写新的 NDIS 微型端口驱动程序时，应编写反序列化的驱动程序。 如果可能，还应将旧驱动程序移植到 NDIS 6.0 或更高版本。 有关移植驱动程序的详细信息，请参阅：

-   [将 NDIS 1.x 驱动程序移植到 NDIS 6。0](/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)
-   [将 NDIS 6.x 驱动程序移植到 NDIS 6.20](porting-ndis-6-x-drivers-to-ndis-6-20.md)
-   [将 NDIS 6.x 驱动程序移植到 NDIS 6.30](porting-ndis-6-x-drivers-to-ndis-6-30.md)

反序列化的微型端口驱动程序在使用 NDIS 进行接口时必须满足以下要求：

-   反序列化的微型端口驱动程序必须在初始化期间将自身标识为此类。

-   反序列化的微型端口驱动程序必须异步完成所有发送请求。 若要完成发送请求，无连接 NDIS 6.0 和更高版本的微型端口驱动程序将调用 **NdisMSendNetBufferListsComplete** 函数。 面向连接的 NDIS 6.0 和更高的微型端口驱动程序调用 **NdisMCoSendNetBufferListsComplete** 函数。

-   支持 NDIS 6.0 或更高版本的反序列化微型**Status**端口驱动程序 \_ \_ 将会传递到**NdisMSendNetBufferListsComplete**的网络缓冲区列表结构的状态成员。

-   如果反序列化的微型端口驱动程序无法立即完成发送请求，它无法将对 NDIS 的请求返回到正在重新排队。 相反，微型端口驱动程序必须在内部将发送请求排队，直到有足够的资源可用于传输数据。

-   反序列化微型端口驱动程序不能在 NDIS 返回它们之前，检查它传递给 NDIS 的结构。 NDIS 将网络 \_ 缓冲区 \_ 列表结构返回到微型端口驱动程序的 *MiniportReturnNetBufferLists* 函数。

反序列化的微型端口驱动程序必须满足以下驱动程序内部要求：

-   反序列化的微型端口驱动程序必须使用 [自旋锁](../kernel/introduction-to-spin-locks.md)保护其网络缓冲区队列。 反序列化的微型端口驱动程序还必须通过其自身的 *MiniportXxx* 函数来保护其共享状态。

-   反序列化的微型端口驱动程序的 *MiniportXxx* 函数可以以 IRQL &lt; = 调度 \_ 级别运行。 因此，驱动程序编写器无法假定 *MiniportXxx* 函数将按它们处理请求的顺序进行调用。 一个 *MiniportXxx* 函数可以抢占以较低的 IRQL 运行的另一个 *MiniportXxx* 函数。

-   反序列化的微型端口驱动程序负责网络缓冲区队列管理。 当微型端口驱动程序遇到资源问题时，它无法将发送请求返回到 NDIS for 正在重新排队。 相反，微型端口驱动程序必须在内部发送所有发送请求，直到有足够的资源可用于发送数据。

-   反序列化的微型端口驱动程序应按照协议确定的顺序完成发送请求。

有关 NDIS 驱动程序的发送和接收要求的详细信息，请参阅 [发送和接收操作](send-and-receive-operations.md)。

请注意，反序列化的微型端口驱动程序通常按协议确定的顺序完成发送请求。 但是，支持数据包优先级的微型端口驱动程序 (例如，IEEE 802.1 p) 可以根据优先级信息对发送请求重新排序。

 

