---
title: 确定网络适配器的 NVGRE 任务卸载功能
description: 本部分介绍如何确定网络适配器的 NVGRE 任务卸载功能
ms.assetid: 1F9C5E7D-5488-47C1-BEDC-D7C640F57511
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e73c3c66ed85679352edcf0c64ea747ddae6502c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834900"
---
# <a name="determining-the-nvgre-task-offload-capabilities-of-a-network-adapter"></a>确定网络适配器的 NVGRE 任务卸载功能


支持[使用通用路由封装（NVGRE）任务卸载的网络虚拟化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)的微型端口驱动程序使用[**NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构来报告此功能[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数传递到[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)。

## <a name="reporting-nvgre-task-offload-capability"></a>报告 NVGRE 任务卸载功能


在[**NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构中，必须按如下所示设置**标头**成员：

-   **修订版**成员必须设置为**NDIS\_卸载\_修订版\_3**。
-   **大小**成员必须设置为**ndis\_SIZEOF\_ndis\_卸载\_修订版本\_3**。

若要报告其对 NVGRE 任务卸载的支持，微型端口驱动程序将 NDIS\_中的以下成员设置为[**封装\_数据包\_任务\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)结构，该结构存储在 EncapsulatedPacketTaskOffloadGre 中。NDIS 驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数传递给[**NDISMSETMINIPORTATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)的[**NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构的成员：

-   将**MaxHeaderSizeSupported**成员设置为所有这些任务卸载的 NIC 必须支持的最大标头大小（tcp 或 udp 有效负载的最大字节数，即 TCP 或 udp 内部标头的最后一个字节）。 协议驱动程序应不会卸载其组合的封装标头超过此大小的数据包的处理。

    **请注意**  256 字节是一个非常好的默认值，应涵盖所有可能的情况。

     

-   设置其他成员，以指示对封装的数据包支持哪些类型的任务卸载微型端口驱动程序。 有关可为这些成员设置的标志的列表，请参阅[ **\_封装\_数据包\_任务**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)的 "备注" 部分，\_卸载。

## <a name="querying-nvgre-task-offload-capability"></a>查询 NVGRE 任务卸载功能


若要确定微型端口驱动程序是否支持 NVGRE 任务卸载，协议和筛选器驱动程序可以[\_TCP\_卸载\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)OID 请求，后者将返回[**NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构。

**请注意**  若要确定微型端口驱动程序的 NVGRE 功能当前是否已启用，请按照查询和更改 NVGRE 任务中所述，使用[OID\_TCP\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)OID 请求[卸载状态](querying-and-changing-nvgre-task-offload-state.md)。

 

**请注意**  若要启用或禁用微型端口驱动程序的 NVGRE 功能，请使用[oid\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)OID 请求，如[查询和更改 NVGRE 任务卸载状态](querying-and-changing-nvgre-task-offload-state.md)中所述。

 

 

 





