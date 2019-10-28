---
title: 访问 IPsec 卸载版本2中的 NET_BUFFER_LIST 信息
description: 访问 IPsec 卸载版本 2 中的 NET_BUFFER_LIST 信息
ms.assetid: 0c27b594-2c61-4459-96df-1d7445100bc5
keywords:
- IPsecOV2 WDK TCP/IP 传输，NET_BUFFER_LIST 信息
- NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ff7547cbb48d2c0a72c74bd8d730032f9b95e83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838254"
---
# <a name="accessing-net_buffer_list-information-in-ipsec-offload-version-2"></a>在 IPsec 卸载版本2中访问 NET\_BUFFER\_列表信息

\[IPsec 任务卸载功能已弃用，不应使用。\]




NDIS 在[**net\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的**NetBufferListInfo**成员中提供带外（OOB）数据，该结构指定[**网络\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的链接列表。 **NetBufferListInfo**成员是值的数组，其中包含列表中所有 NET\_缓冲区结构共有的信息。

使用以下标识符和[**NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)宏来设置和获取**NetBufferListInfo**数组中的 IPsec 卸载版本2（IPsecOV2） OOB 数据：

<a href="" id="ipsecoffloadv2netbufferlistinfo"></a>**IPsecOffloadV2NetBufferListInfo**  
指定在将 IPsec 任务从 TCP/IP 协议卸载到 NIC 时使用的 IPsecOV2 信息。 指定**IPsecOffloadV2NetBufferListInfo**时，NET\_BUFFER\_列表\_信息返回[**NDIS\_IPSEC\_卸载\_\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)构造.

<a href="" id="ipsecoffloadv2tunnelnetbufferlistinfo"></a>**IPsecOffloadV2TunnelNetBufferListInfo**  
指定在将 IPsec 任务从 TCP/IP 协议卸载到 NIC 时使用的 IPsecOV2 隧道信息。 指定**IPsecOffloadV2TunnelNetBufferListInfo**时，NET\_BUFFER\_列表\_信息返回[ **\_IPSEC\_\_\_\_隧道\__t_13_ 信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_tunnel_net_buffer_list_info)结构。

<a href="" id="ipsecoffloadv2headernetbufferlistinfo"></a>**IPsecOffloadV2HeaderNetBufferListInfo**  
指定[**NET\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中 IPsec 标头的标头偏移量，以及下一个标头和填充长度的值。 指定**IPsecOffloadV2HeaderNetBufferListInfo**时，NET\_BUFFER\_列表\_信息返回[ **\_IPSEC\_\_\_\_\_\_\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info)结构。

 

 





