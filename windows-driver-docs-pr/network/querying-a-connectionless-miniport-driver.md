---
title: 查询无连接微型端口驱动程序
description: 查询无连接微型端口驱动程序
keywords:
- 无连接驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38e175feb9700da8a58db77338fb0fb670e8bcae
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248735"
---
# <a name="querying-a-connectionless-miniport-driver"></a>查询无连接微型端口驱动程序





为了查询无连接微型端口驱动程序维护的 Oid，绑定协议会调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) ，并传递 [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request) 结构，该结构指定正在查询的对象 (OID) ，并指向 ndis 最终写入请求信息的缓冲区。

如果 NDIS 驱动程序没有响应，则对 **NdisOidRequest** 的调用会使 NDIS 调用微型端口驱动程序的 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数，从而将请求的信息返回到 NDIS。 *MiniportOidRequest* 可以通过调用 [**NdisMOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)同步或异步完成。

NDIS 还可以代表自己调用微型端口驱动程序的 *MiniportOidRequest* 函数-例如，在微型端口驱动程序的 *MiniportInitializeEx* 函数返回了 NDIS 状态 SUCCESS 后，便可 \_ \_ 查询微型端口驱动程序的功能、状态或统计信息。 下图说明了如何查询无连接微型端口驱动程序。

![说明如何查询无连接微型端口驱动程序的示意图](images/fig5-2.png)

NDIS 代表微型端口驱动程序响应多个 OID 请求。 微型端口驱动程序在初始化和状态指示过程中报告其所有 OID 值。 有关在属性中报告的 OID 值的详细信息，请参阅 [**NDIS \_ 微型端口 \_ 适配器 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_attributes) 和相关的属性结构。

当使用 OID \_ GEN MAC 选项调用 MiniportOidRequest 时 \_ \_ ，它必须返回一个位掩码，该位掩码指定微型端口驱动程序执行的可选操作。 标志集包括：

-   NDIS \_ MAC \_ 选项 \_ 复制 \_ 预测先行 \_ 数据。 此标志向协议驱动程序指示它可以通过任何方式访问指定的数据。 如果微型端口驱动程序指示数据超出了机载共享内存，则它不能设置此标志。

-   NDIS \_ MAC \_ 选项 \_ 无 \_ 环回。 如果设置了此标志，则微型端口驱动程序不会环回传递到 *MiniportSendNetBufferLists (数据包* 的数据包，这些) 数据包将定向到同一台计算机上的接收方，并要求 NDIS 驱动程序执行环回。 如果 NDIS 执行数据包环回，数据包将不会向下传递到微型端口驱动程序。 小型端口驱动程序始终设置此标志，除非 NIC 执行硬件环回。

-   NDIS \_ MAC \_ 选项 \_ 接收已 \_ 序列化。 如果设置了此标志，微型端口驱动程序将不会显示任何新接收的数据包，直到先前接收到的数据包经过完全处理（包括传输数据）为止。 大多数微型端口驱动程序（用于指示通过调用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)的数据包的驱动程序除外）设置此标志。

微型端口驱动程序绝不能使用 \_ \_ 保留的 "用于 ndis 内部使用的标记 ndis MAC 选项" \_ 。

还会使用特定于媒体的 OID 来查询 *MiniportOidRequest* ，以确定 NIC 的当前地址。 例如，将查询802.3 类型的 NIC 的微型端口驱动程序，并使用 OID \_ 802 \_ 3 \_ 当前 \_ 地址。

某些媒体类型的微型端口驱动程序将接收特定于媒体的其他 Oid。 例如，查询 NIC 为802.3 类型的微型端口驱动程序，并使用 OID \_ 802.3 \_ 最大 \_ 列表 \_ 大小进行查询。 有关详细信息，请参阅 [常规对象](/previous-versions/windows/hardware/network/ff546510(v=vs.85))。

 

