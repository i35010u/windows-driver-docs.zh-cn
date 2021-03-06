---
title: 访问 IPsec 卸载版本2中的 NET_BUFFER_LIST 信息
description: 访问 IPsec 卸载版本 2 中的 NET_BUFFER_LIST 信息
keywords:
- IPsecOV2 WDK TCP/IP 传输，NET_BUFFER_LIST 信息
- NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c98a2dc8378b616b3b718ac6f01a609e1103e8f7
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249306"
---
# <a name="accessing-net_buffer_list-information-in-ipsec-offload-version-2"></a>访问 \_ \_ IPsec 卸载版本2中的网络缓冲区列表信息

\[IPsec 任务卸载功能已弃用，不应使用。\]




NDIS 提供 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)结构的 **NetBufferListInfo** 成员中的带外 (OOB) 数据，该结构指定 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer)结构的链接列表。 **NetBufferListInfo** 成员是值的数组，其中包含列表中所有网络缓冲区结构共有的信息 \_ 。

将以下标识符与 [**NET \_ BUFFER \_ LIST \_ INFO**](/windows-hardware/drivers/ddi/nblaccessors/nf-nblaccessors-net_buffer_list_info) 宏一起使用，以在 **NetBufferListInfo** 数组中设置和获取 IPSEC 卸载版本 2 (IPsecOV2) OOB 数据：

<a href="" id="ipsecoffloadv2netbufferlistinfo"></a>**IPsecOffloadV2NetBufferListInfo**  
指定在将 IPsec 任务从 TCP/IP 协议卸载到 NIC 时使用的 IPsecOV2 信息。 指定 **IPsecOffloadV2NetBufferListInfo** 时，网络 \_ 缓冲区 \_ 列表 \_ 信息将返回 [**NDIS \_ IPSEC \_ 卸载 \_ V2 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info) 结构。

<a href="" id="ipsecoffloadv2tunnelnetbufferlistinfo"></a>**IPsecOffloadV2TunnelNetBufferListInfo**  
指定在将 IPsec 任务从 TCP/IP 协议卸载到 NIC 时使用的 IPsecOV2 隧道信息。 指定 **IPsecOffloadV2TunnelNetBufferListInfo** 时，网络 \_ 缓冲区 \_ 列表 \_ 信息将返回 [**NDIS \_ IPSEC \_ 卸载 \_ V2 \_ 隧道 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_tunnel_net_buffer_list_info) 结构。

<a href="" id="ipsecoffloadv2headernetbufferlistinfo"></a>**IPsecOffloadV2HeaderNetBufferListInfo**  
指定 [**NET \_ BUFFER \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 中 IPsec 标头的标头偏移量以及下一个标头和填充长度的值。 指定 **IPsecOffloadV2HeaderNetBufferListInfo** 时，网络 \_ 缓冲区 \_ 列表 \_ 信息将返回 [**NDIS \_ IPSEC \_ 卸载 \_ V2 \_ 标头 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info) 结构。

 

