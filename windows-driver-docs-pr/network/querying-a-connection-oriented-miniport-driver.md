---
title: 查询面向连接的微型端口驱动程序
description: 查询面向连接的微型端口驱动程序
keywords:
- 面向连接的驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 458039c4c0d161d60c982f1f3057e7a8427dde49
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247847"
---
# <a name="querying-a-connection-oriented-miniport-driver"></a>查询面向连接的微型端口驱动程序





若要查询面向连接的微型端口驱动程序维护的信息对象，绑定协议将调用 [**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) ，并传递一个 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request) 结构，该结构指定正在查询的对象 (OID) ，并提供一个缓冲区，ndis 最终写入请求的信息。 对 **NdisCoOidRequest** 的调用会使 NDIS 调用微型端口驱动程序的 [*MiniportCoOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request) 函数，该函数将请求的信息返回到 NDIS。 *MiniportCoOidRequest* 可以通过调用 [**NdisCoOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequestcomplete)同步或异步完成。

NDIS 还可以代表自己调用微型端口驱动程序的 [*MiniportCoOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request) 函数，例如，在微型端口驱动程序的 [*MINIPORTINITIALIZEEX*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数返回 NDIS 状态 "成功" 后， \_ \_ 查询微型端口驱动程序的功能、状态或统计信息。 下图说明了如何查询面向连接的微型端口驱动程序。

![说明查询面向连接的微型端口驱动程序的示意图](images/fig5-3.png)

面向连接的微型端口驱动程序必须能够为特定 NIC (VCs) 的所有虚拟连接提供全局基础信息，还可以为每个 VC 提供相关信息。 例如，如果向 [*MiniportCoOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)提供了一个非 **NULL** *NdisVcHandle* ，用于执行 [OID \_ GEN \_ 共同 \_ RCV \_ CRC \_ 错误](./oid-gen-co-rcv-crc-error.md)的查询，则微型端口驱动程序将返回在指定的 VC 上的所有接收中遇到的 CRC 错误的数目。 对于具有 **NULL** *NdisVcHandle* 的同一请求，微型端口驱动程序将返回通过 NIC 的所有传入接收所遇到的 CRC 错误总数。

下面的列表包含面向连接的微型端口驱动程序的必需常规操作 Oid 集：

[OID \_ GEN \_ 共同 \_ 支持的 \_ 列表](./oid-gen-co-supported-list.md)

[OID \_ 生成 \_ 共同 \_ 硬件 \_ 状态](./oid-gen-co-hardware-status.md)

[\_支持 OID GEN \_ 共同 \_ 媒体 \_](./oid-gen-co-media-supported.md)

[\_ \_ \_ \_ 正在使用 OID 生成 CO \_ 媒体](./oid-gen-co-media-in-use.md)

[OID \_ 代 \_ 共同 \_ 链接 \_ 速度](./oid-gen-co-link-speed.md)

[OID \_ GEN \_ 共同 \_ 供应商 \_ ID](./oid-gen-co-vendor-id.md)

[OID \_ GEN \_ 共同 \_ 供应商 \_ 说明](./oid-gen-co-vendor-description.md)

[OID \_ GEN \_ 共同 \_ 供应商 \_ 驱动程序 \_ 版本](./oid-gen-co-vendor-driver-version.md)

[OID \_ GEN \_ 共同 \_ 驱动程序 \_ 版本](./oid-gen-co-driver-version.md)

[OID \_ GEN \_ 共同 \_ MAC \_ 选项](./oid-gen-co-mac-options.md)

[OID \_ 生成 \_ CO \_ 媒体 \_ 连接 \_ 状态](./oid-gen-co-media-connect-status.md)

[OID \_ GEN \_ 共同的 \_ 最小 \_ 链接 \_ 速度](./oid-gen-co-minimum-link-speed.md)

小型端口驱动程序的 [*MiniportCoOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request) 函数必须准备好响应查询或将其设置为上述任何 oid。

当[](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)使用 OID \_ GEN \_ 共同 MAC 选项调用 MiniportCoOidRequest 时 \_ \_ ，它必须返回一个位掩码，该位掩码指定微型端口驱动程序执行的可选操作。 标志集包括：

-   NDIS \_ MAC \_ 选项 \_ 无 \_ 环回。 如果设置了此标志，则微型端口驱动程序不会环回传递到 [**MiniportCoSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists) 的数据包，该数据包将定向到同一台计算机上的接收方，并且微型端口驱动程序要求 NDIS 执行环回。 如果 NDIS 执行数据包环回，数据包将不会向下传递到微型端口驱动程序。 小型端口驱动程序始终设置此标志，除非 NIC 执行硬件环回。

-   NDIS \_ MAC \_ ETOX \_ 指示。 如果设置此标志，则微型端口驱动程序指示仅在 NIC 传输数据包后发送完成。

微型端口驱动程序绝不能使用 NDIS \_ MAC \_ 选项 \_ 保留标志，该标志是为 NDIS 内部使用保留的。

还将使用特定于媒体的 OID 来查询 [*MiniportCoOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request) ，以确定 NIC 的当前地址。

有关详细信息，请参阅 [Connection-Oriented 调用管理器和客户端](./oids-for-connection-oriented-call-managers-and-clients.md) 以及 [常规对象](/previous-versions/windows/hardware/network/ff546510(v=vs.85))的 oid。

 

