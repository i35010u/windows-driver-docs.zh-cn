---
title: 确定网络适配器的 RSC 功能
description: 接收段合并 (RSC)-支持的微型端口驱动程序通过将其传递到 NdisMSetMiniportAttributes NDIS_OFFLOAD 结构报告其 RSC 功能。
ms.assetid: 043A09F9-7D5D-4401-9645-19FDBD614659
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 196cbecacfe3b18f64849a3b7bfa2a0e96a271c5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381414"
---
# <a name="determining-the-rsc-capabilities-of-a-network-adapter"></a>确定网络适配器的 RSC 功能


接收段合并 (RSC)-支持的微型端口驱动程序报告通过其 RSC 功能[ **NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构，它将传递给[ **NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)。

## <a name="reporting-rsc-capability"></a>报告 RSC 功能


在中[ **NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构**标头**成员必须按如下所示设置：

-   **修订**成员必须设置为**NDIS\_卸载\_修订\_3**。
-   **大小**成员必须设置为**NDIS\_SIZEOF\_NDIS\_卸载\_修订\_3**。

若要报告其支持适用于 RSC，微型端口驱动程序可以设置以下成员[ **NDIS\_TCP\_收到\_SEG\_COALESCE\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_recv_seg_coalesce_offload)结构，它存储在**Rsc**的成员[ **NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构：

-   设置**IPv4.Enabled**成员添加到**TRUE**以指示对 IPv4 的 RSC 的支持。

-   设置**IPv6.Enabled**成员添加到**TRUE**以指示对 IPv6 的 RSC 的支持。

微型端口驱动程序必须至少支持 RSC 的 IEEE 802.3 封装。 此外，它可以支持任何其他封装 RSC。 如果不支持一些封装，RSC 并接收该封装的数据包，驱动程序必须在通常指示在堆栈中向上的数据包。

## <a name="querying-rsc-capability"></a>查询 RSC 功能


若要确定微型端口驱动程序是否支持 RSC，协议驱动程序和其他驱动程序可以发出[OID\_TCP\_卸载\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)OID 请求，它将返回[ **NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构。

 

 





