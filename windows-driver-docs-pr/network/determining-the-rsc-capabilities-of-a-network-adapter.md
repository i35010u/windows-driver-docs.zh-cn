---
title: 确定网络适配器的 RSC 功能
description: 接收段合并（RSC）的微型端口驱动程序通过其传递到 NdisMSetMiniportAttributes 的 NDIS_OFFLOAD 结构报告其 RSC 功能。
ms.assetid: 043A09F9-7D5D-4401-9645-19FDBD614659
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5b63cf8a3fdd22fe4aa13e9afef078cd09a42f4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838146"
---
# <a name="determining-the-rsc-capabilities-of-a-network-adapter"></a>确定网络适配器的 RSC 功能


支持接收段合并（RSC）的微型端口驱动程序通过将[**NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构传递到[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)来报告其 RSC 功能。

## <a name="reporting-rsc-capability"></a>报告 RSC 功能


在[**NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构中，必须按如下所示设置**标头**成员：

-   **修订版**成员必须设置为**NDIS\_卸载\_修订版\_3**。
-   **大小**成员必须设置为**ndis\_SIZEOF\_ndis\_卸载\_修订版本\_3**。

若要报告其对 RSC 的支持，小型端口驱动程序可以在 Ndis 中设置以下成员[ **\_TCP\_接收\_SEG\_合并\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_recv_seg_coalesce_offload)结构，该结构存储在 NDIS 的**RSC**成员[ **\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构：

-   将 "**已启用**" 成员设置为**TRUE** ，以指示支持适用于 RSC 的 ipv4。

-   将 "**已启用 ipv6** " 成员设置为**TRUE** ，以指示支持对 RSC for IPv6 的支持。

小型端口驱动程序必须至少支持 IEEE 802.3 封装中的 RSC。 此外，它还可以支持任何其他封装的 RSC。 如果它不支持用于某些封装的 RSC，并收到该封装的数据包，则驱动程序必须正常指示堆栈上的数据包。

## <a name="querying-rsc-capability"></a>正在查询 RSC 功能


若要确定微型端口驱动程序是否支持 RSC，协议驱动程序和其他驱动程序可以颁发[oid\_TCP\_卸载\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-hardware-capabilities)OID 请求，这将返回[**NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)构造.

 

 





