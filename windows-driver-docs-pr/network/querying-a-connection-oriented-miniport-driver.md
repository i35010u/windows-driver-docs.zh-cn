---
title: 查询面向连接的微型端口驱动程序
description: 查询面向连接的微型端口驱动程序
ms.assetid: 9e9926f6-cf90-48af-885f-59725721948d
keywords:
- 面向连接的驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0704eeca1ee5ce7934a26a951a62014c3eefa2df
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844904"
---
# <a name="querying-a-connection-oriented-miniport-driver"></a>查询面向连接的微型端口驱动程序





若要查询面向连接的微型端口驱动程序维护的信息对象，绑定协议将调用[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) ，并将[**NDIS\_OID 传递\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构，该结构指定正在查询的对象（OID）和，它提供了一个缓冲区，NDIS 最终会在其中写入所请求的信息。 对**NdisCoOidRequest**的调用会使 NDIS 调用微型端口驱动程序的[*MiniportCoOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)函数，该函数将请求的信息返回到 NDIS。 *MiniportCoOidRequest*可以通过调用[**NdisCoOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)同步或异步完成。

NDIS 还可以代表自己调用微型端口驱动程序的[*MiniportCoOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)函数，例如，在微型端口驱动程序的[*MINIPORTINITIALIZEEX*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数返回 NDIS\_状态时\_SUCCESS）查询微型端口驱动程序的功能、状态或统计信息。 下图说明了如何查询面向连接的微型端口驱动程序。

![说明查询面向连接的微型端口驱动程序的示意图](images/fig5-3.png)

面向连接的微型端口驱动程序必须能够为特定 NIC 的所有虚拟连接（VCs）以及每个 VC 提供全局基础信息。 例如，如果向[*MiniportCoOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)提供了一个非**NULL** *NDISVCHANDLE*以查找[OID\_代\_CO\_RCV\_CRC\_错误](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-rcv-crc-error)，则微型端口驱动程序将返回 crc 错误的数目在指定的 VC 上的所有接收中都遇到。 对于具有**NULL** *NdisVcHandle*的同一请求，微型端口驱动程序将返回通过 NIC 的所有传入接收所遇到的 CRC 错误总数。

下面的列表包含面向连接的微型端口驱动程序的必需常规操作 Oid 集：

[OID\_代\_共同\_支持\_列表](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-supported-list)

[OID\_代\_共同\_硬件\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-hardware-status)

[支持 OID\_代\_联\_媒体\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-media-supported)

[OID\_代\_联\_媒体\_在\_中使用](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-media-in-use)

[OID\_代\_联\_链接\_速度](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-link-speed)

[OID\_代\_联\_供应商\_ID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-vendor-id)

[OID\_代\_联合\_供应商\_说明](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-vendor-description)

[OID\_代\_联合\_供应商\_驱动程序\_版本](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-vendor-driver-version)

[OID\_代\_CO\_驱动程序\_版本](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-driver-version)

[OID\_代\_联\_MAC\_选项](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-mac-options)

[OID\_代\_联\_媒体\_连接\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-media-connect-status)

[OID\_代\_联\_最小\_链接\_速度](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-minimum-link-speed)

小型端口驱动程序的[*MiniportCoOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)函数必须准备好响应查询或将其设置为上述任何 oid。

当使用 OID\_GEN\_CO\_MAC\_选项调用[*MiniportCoOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)时，它必须返回一个位掩码，该位掩码指定微型端口驱动程序执行的可选操作。 标志集包括：

-   NDIS\_MAC\_选项\_不\_环回。 如果设置了此标志，则微型端口驱动程序不会环回传递到[**MiniportCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists)的数据包，该数据包将定向到同一台计算机上的接收方，并且微型端口驱动程序要求 NDIS 执行环回。 如果 NDIS 执行数据包环回，数据包将不会向下传递到微型端口驱动程序。 小型端口驱动程序始终设置此标志，除非 NIC 执行硬件环回。

-   NDIS\_MAC\_ETOX\_指示。 如果设置此标志，则微型端口驱动程序指示仅在 NIC 传输数据包后发送完成。

小型端口驱动程序绝不能使用 NDIS\_MAC\_选项\_保留标志，该标志是为 NDIS 内部使用保留的。

还将使用特定于媒体的 OID 来查询[*MiniportCoOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request) ，以确定 NIC 的当前地址。

有关详细信息，请参阅[面向连接的呼叫管理器和客户端的 oid](https://docs.microsoft.com/windows-hardware/drivers/network/oids-for-connection-oriented-call-managers-and-clients)和[常规对象](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546510(v=vs.85))。

 

 





