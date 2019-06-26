---
title: 确定网络适配器的 NVGRE 任务卸载功能
description: 本部分介绍如何确定网络适配器的 NVGRE 任务卸载功能
ms.assetid: 1F9C5E7D-5488-47C1-BEDC-D7C640F57511
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b63c6222f98f1f1f08d8a8a1bbffb2344c479d4b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381395"
---
# <a name="determining-the-nvgre-task-offload-capabilities-of-a-network-adapter"></a>确定网络适配器的 NVGRE 任务卸载功能


支持的微型端口驱动程序[网络虚拟化使用通用路由封装 (NVGRE) 任务卸载](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)报告通过此功能[ **NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构，其[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数将传递给[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes).

## <a name="reporting-nvgre-task-offload-capability"></a>报告 NVGRE 任务卸载功能


在中[ **NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构**标头**成员必须按如下所示设置：

-   **修订**成员必须设置为**NDIS\_卸载\_修订\_3**。
-   **大小**成员必须设置为**NDIS\_SIZEOF\_NDIS\_卸载\_修订\_3**。

若要报告其支持 NVGRE 任务卸载，微型端口驱动程序设置以下中的成员[ **NDIS\_封装\_数据包\_任务\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)结构，它存储在**EncapsulatedPacketTaskOffloadGre**的成员[ **NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构微型端口驱动程序[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数将传递给[ **NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes):

-   设置**MaxHeaderSizeSupported**成员添加到的最大标头大小从开头到开头的内部 TCP 或 UDP 负载 （TCP 或 UDP 内部标头的最后一个字节） 的 NIC 必须支持所有这些任务数据包将卸载。 协议驱动程序应不卸载其组合的封装标头超过此大小的数据包的处理。

    **请注意**  256 个字节是一个很好的默认值，应涵盖所有可能情况。

     

-   设置的其他成员来指示哪些类型的任务卸载封装的数据包微型端口驱动程序支持。 可以为这些成员中设置的标志的列表，请参阅备注部分[ **NDIS\_封装\_数据包\_任务\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)。

## <a name="querying-nvgre-task-offload-capability"></a>查询 NVGRE 任务卸载功能


若要确定微型端口驱动程序是否支持 NVGRE 任务卸载，协议和筛选器驱动程序可以发出[OID\_TCP\_卸载\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)OID 请求它将返回[ **NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构。

**请注意**  若要确定微型端口驱动程序的 NVGRE 功能当前是否已启用，请使用[OID\_TCP\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)OID 请求中所述[查询和更改 NVGRE 任务卸载状态](querying-and-changing-nvgre-task-offload-state.md)。

 

**请注意**  若要启用或禁用微型端口驱动程序的 NVGRE 功能，使用[OID\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)OID 请求中所述[查询和更改 NVGRE 任务卸载状态](querying-and-changing-nvgre-task-offload-state.md)。

 

 

 





