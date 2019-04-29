---
title: 查询无连接微型端口驱动程序
description: 查询无连接微型端口驱动程序
ms.assetid: a556d7ba-52ea-443b-994b-4c517e80ac55
keywords:
- 无连接驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5fa9bf331d82c2d8be871e9efb1ca221f5acef9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366505"
---
# <a name="querying-a-connectionless-miniport-driver"></a>查询无连接微型端口驱动程序





若要查询的无连接的微型端口驱动程序维护的 Oid，绑定的协议调用[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710) ，并将传递[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构，它指定的对象 (OID) 正被查询的和，它指向在其中 NDIS 最终写入所需的信息的缓冲区。

如果 NDIS 不响应的微型端口驱动程序，在调用**NdisOidRequest**会导致调用微型端口驱动程序的 NDIS [ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)函数，该返回函数到 NDIS 所需的信息。 *MiniportOidRequest*可以通过调用完成同步或异步[ **NdisMOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563622)。

NDIS 还可以调用微型端口驱动程序*MiniportOidRequest*代表其自身-例如后微型端口驱动程序的, 函数*MiniportInitializeEx*函数已返回 NDIS\_状态\_成功--若要查询微型端口驱动程序的功能、 状态或统计信息。 下图说明了查询无连接的微型端口驱动程序。

![说明查询无连接的微型端口驱动程序的关系图](images/fig5-2.png)

NDIS 代表微型端口驱动程序的很多 OID 请求做出响应。 微型端口驱动程序报告的许多其 OID 值在初始化过程并在状态指示。 有关 OID 的值的属性中报告的详细信息，请参阅[ **NDIS\_微型端口\_适配器\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565920)和相关的属性结构。

当*MiniportOidRequest*调用时所使用 OID\_常规\_MAC\_选项，它必须返回一个位掩码，指定可选的微型端口驱动程序所执行的操作。 将该组标志包括：

-   NDIS\_MAC\_选项\_副本\_预测先行\_数据。 此标志指示协议驱动程序，它可以通过任何方式访问所指示的数据。 如果微型端口驱动程序指示数据载入共享内存不足，它必须不设置此标志。

-   NDIS\_MAC\_选项\_否\_环回。 如果设置此标志，微型端口驱动程序不传递到的数据包会不环回*MiniportSendNetBufferLists(Packets)* 的定向到同一台计算机上接收方和微型端口驱动程序需要执行的 NDIS环回。 如果 NDIS 执行数据包的环回，数据包不传递给微型端口驱动程序。 除非 NIC 执行硬件环回，微型端口驱动程序始终会设置此标志。

-   NDIS\_MAC\_选项\_接收\_已序列化。 如果设置此标志，微型端口驱动程序并不表示任何新收到的数据包之前以前接收的数据包已完全处理，包括将数据传输。 大多数微型端口驱动程序，除非那些向上数据包通过调用指示[ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)，设置此标志。

微型端口驱动程序必须永远不会使用标志 NDIS\_MAC\_选项\_保留，保留供 NDIS 内部使用。

*MiniportOidRequest*也查询具有特定于媒体的 OID，若要确定当前地址的 NIC。 例如，802.3 类型的 NIC 的微型端口驱动程序将查询与 OID\_802\_3\_当前\_地址。

某些媒体类型的微型端口驱动程序将收到其他媒体特定于的 Oid。 例如，其 NIC 是类型 802.3 的微型端口驱动程序查询具有 OID\_802.3\_最大\_列表\_大小。 有关详细信息，请参阅[常规对象](https://msdn.microsoft.com/library/windows/hardware/ff546510)。

 

 





