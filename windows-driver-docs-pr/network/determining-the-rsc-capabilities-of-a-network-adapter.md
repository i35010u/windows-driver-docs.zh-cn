---
title: 确定网络适配器的 RSC 功能
description: 接收段合并 (RSC) 功能的微型端口驱动程序通过它传递给 NdisMSetMiniportAttributes 的 NDIS_OFFLOAD 结构报告其 RSC 功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33dd81ce924b764402a9455a9670c303e2ab37f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830347"
---
# <a name="determining-the-rsc-capabilities-of-a-network-adapter"></a>确定网络适配器的 RSC 功能


接收段合并 (RSC) 功能的微型端口驱动程序通过它传递给 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)的 [**NDIS \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构报告其 RSC 功能。

## <a name="reporting-rsc-capability"></a>报告 RSC 功能


在 [**NDIS \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload) 结构中，必须按如下所示设置 **标头** 成员：

-   **修订** 成员必须设置为 **NDIS \_ 卸载 \_ 修订版本 \_ 3**。
-   **Size** 成员必须设置为 **ndis \_ SIZEOF \_ ndis \_ 卸载 \_ 修订版 \_ 3**。

若要报告其对 RSC 的支持，小型端口驱动程序可以在 [**ndis \_ TCP \_ 接收 \_ SEG \_ 合并 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_recv_seg_coalesce_offload)结构中设置以下成员，该结构存储在 [**ndis \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构的 **RSC** 成员中：

-   将 " **已启用** " 成员设置为 **TRUE** ，以指示支持适用于 RSC 的 ipv4。

-   将 " **已启用 ipv6** " 成员设置为 **TRUE** ，以指示支持对 RSC for IPv6 的支持。

小型端口驱动程序必须至少支持 IEEE 802.3 封装中的 RSC。 此外，它还可以支持任何其他封装的 RSC。 如果它不支持用于某些封装的 RSC，并收到该封装的数据包，则驱动程序必须正常指示堆栈上的数据包。

## <a name="querying-rsc-capability"></a>正在查询 RSC 功能


若要确定微型端口驱动程序是否支持 RSC，协议驱动程序和其他驱动程序可以发出 [oid \_ TCP \_ 卸载 \_ 硬件 \_ 功能](./oid-tcp-offload-hardware-capabilities.md) Oid 请求，这将返回 [**NDIS \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload) 结构。

 

