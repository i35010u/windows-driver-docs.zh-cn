---
title: 查询无连接微型端口驱动程序
description: 查询无连接微型端口驱动程序
ms.assetid: a556d7ba-52ea-443b-994b-4c517e80ac55
keywords:
- 无连接驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f4a0e0fa2ff4479b8c1e19e4aed346f343a8b75
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844902"
---
# <a name="querying-a-connectionless-miniport-driver"></a>查询无连接微型端口驱动程序





为了查询无连接微型端口驱动程序维护的 Oid，绑定协议会调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) ，并将[**NDIS\_OID 传递\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构，该结构指定正在查询的对象（OID），并指向缓冲区其中，NDIS 最终会写入请求的信息。

如果 NDIS 驱动程序没有响应，则对**NdisOidRequest**的调用会使 NDIS 调用微型端口驱动程序的[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数，从而将请求的信息返回到 NDIS。 *MiniportOidRequest*可以通过调用[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)同步或异步完成。

此外，NDIS 还可以代表自己调用微型端口驱动程序的*MiniportOidRequest*函数-例如，在微型端口驱动程序的*MINIPORTINITIALIZEEX*函数返回 NDIS\_状态后\_SUCCESS，以查询小型端口驱动程序的功能、状态或统计信息。 下图说明了如何查询无连接微型端口驱动程序。

![说明如何查询无连接微型端口驱动程序的示意图](images/fig5-2.png)

NDIS 代表微型端口驱动程序响应多个 OID 请求。 微型端口驱动程序在初始化和状态指示过程中报告其所有 OID 值。 有关在属性中报告的 OID 值的详细信息，请参阅[**NDIS\_微型端口\_适配器\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_attributes)和相关的属性结构。

当使用 OID\_GEN\_MAC\_选项调用*MiniportOidRequest*时，它必须返回一个位掩码，该位掩码指定微型端口驱动程序执行的可选操作。 标志集包括：

-   NDIS\_MAC\_选项\_复制\_预测先行\_数据。 此标志向协议驱动程序指示它可以通过任何方式访问指定的数据。 如果微型端口驱动程序指示数据超出了机载共享内存，则它不能设置此标志。

-   NDIS\_MAC\_选项\_不\_环回。 如果设置了此标志，则微型端口驱动程序不会环回传递到*MiniportSendNetBufferLists （数据包）* 的数据包，该数据包将定向到同一台计算机上的接收方，并且微型端口驱动程序需要 NDIS 才能执行环回。 如果 NDIS 执行数据包环回，数据包将不会向下传递到微型端口驱动程序。 小型端口驱动程序始终设置此标志，除非 NIC 执行硬件环回。

-   NDIS\_MAC\_选项\_接收\_序列化。 如果设置了此标志，微型端口驱动程序将不会显示任何新接收的数据包，直到先前接收到的数据包经过完全处理（包括传输数据）为止。 大多数微型端口驱动程序（用于指示通过调用[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)的数据包的驱动程序除外）设置此标志。

小型端口驱动程序绝不能使用标记 NDIS\_MAC\_选项\_保留，这是为 NDIS 内部使用而保留的。

还会使用特定于媒体的 OID 来查询*MiniportOidRequest* ，以确定 NIC 的当前地址。 例如，将使用 OID\_802\_3\_当前\_地址查询802.3 类型的 NIC 的微型端口驱动程序。

某些媒体类型的微型端口驱动程序将接收特定于媒体的其他 Oid。 例如，使用 OID 查询其 NIC 为802.3 类型的微型端口驱动程序，\_802.3\_最大\_列表\_大小。 有关详细信息，请参阅[常规对象](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546510(v=vs.85))。

 

 





