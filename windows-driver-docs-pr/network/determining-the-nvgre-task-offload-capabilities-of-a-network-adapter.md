---
title: 确定网络适配器的 NVGRE 任务卸载功能
description: 本部分介绍如何确定网络适配器的 NVGRE 任务卸载功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cd3691d45bc37295a48e3ecfad28feb11804984
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838849"
---
# <a name="determining-the-nvgre-task-offload-capabilities-of-a-network-adapter"></a>确定网络适配器的 NVGRE 任务卸载功能


支持 [使用通用路由封装的网络虚拟化的微型端口驱动程序 (NVGRE) 任务卸载](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)通过 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数传递到 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)的 [**NDIS \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构来报告此功能。

## <a name="reporting-nvgre-task-offload-capability"></a>报告 NVGRE 任务卸载功能


在 [**NDIS \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload) 结构中，必须按如下所示设置 **标头** 成员：

-   **修订** 成员必须设置为 **NDIS \_ 卸载 \_ 修订版本 \_ 3**。
-   **Size** 成员必须设置为 **ndis \_ SIZEOF \_ ndis \_ 卸载 \_ 修订版 \_ 3**。

若要报告其对 NVGRE 任务卸载的支持，微型端口驱动程序在 Ndis 的 [**\_ \_ 数据包 \_ 任务 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)结构中设置以下成员，该结构存储在微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数传递给 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)的 [**ndis \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构的 **EncapsulatedPacketTaskOffloadGre** 成员中：

-   将 **MaxHeaderSizeSupported** 成员设置为 TCP 或 udp 有效负载的最大标头大小（TCP 或 udp 负载) 的最大标头大小） (NIC 必须支持所有这些任务卸载的最后一个字节。 协议驱动程序应不会卸载其组合的封装标头超过此大小的数据包的处理。

    **注意**  256 字节是一个非常好的默认值，应涵盖所有可能的情况。

     

-   设置其他成员，以指示对封装的数据包支持哪些类型的任务卸载微型端口驱动程序。 有关可为这些成员设置的标志的列表，请参阅 [**NDIS \_ 封装的 \_ 数据包 \_ 任务 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)的 "备注" 部分。

## <a name="querying-nvgre-task-offload-capability"></a>查询 NVGRE 任务卸载功能


若要确定微型端口驱动程序是否支持 NVGRE 任务卸载，协议和筛选器驱动程序可以发出 [oid \_ TCP \_ 卸载 \_ 硬件 \_ 功能](./oid-tcp-offload-hardware-capabilities.md) Oid 请求，这会返回 [**NDIS \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload) 结构。

**注意**  若要确定是否当前启用了微型端口驱动程序的 NVGRE 功能，请使用 [OID \_ TCP \_ 卸载 \_ 当前的 \_ 配置](./oid-tcp-offload-current-config.md) OID 请求，如 [查询和更改 NVGRE 任务卸载状态](querying-and-changing-nvgre-task-offload-state.md)中所述。

 

**注意**  若要启用或禁用微型端口驱动程序的 NVGRE 功能，请使用 [oid \_ TCP \_ 卸载 \_ 参数](./oid-tcp-offload-parameters.md) oid 请求，如 [查询和更改 NVGRE 任务卸载状态](querying-and-changing-nvgre-task-offload-state.md)中所述。

 

 

