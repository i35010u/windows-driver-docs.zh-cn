---
title: 访问 TCP/IP 卸载 NET_BUFFER_LIST 信息
description: 访问 TCP/IP 卸载 NET_BUFFER_LIST 信息
ms.assetid: 555c9533-ab3f-43f0-9139-b1de33a6b1a7
keywords:
- TCP/IP 卸载 WDK 网络连接、 带外数据
- 卸载 WDK TCP/IP 传输，WDK TCP/IP 卸载的带外数据
- OOB 数据 WDK TCP/IP 卸载
- NET_BUFFER_LIST
- 任务卸载，WDK TCP/IP 传输，带外数据
- 连接将卸载 WDK TCP/IP 传输，带外数据
ms.date: 10/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: 48c2eacd25e671b5d43203ecefd8ccf432fa5c67
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384424"
---
# <a name="accessing-tcpip-offload-netbufferlist-information"></a>访问 TCP/IP 卸载 NET\_缓冲区\_列出信息

NDIS 6.0 及更高版本提供 TCP/IP 卸载带外 (OOB) 中的数据**NetBufferListInfo**的成员[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构，它指定的链接的列表[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构。 **NetBufferListInfo**成员是包含信息普遍适用于 NET 的所有值的数组\_缓冲区列表中的结构。

使用具有以下标识符[ **NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)宏来设置和获取 TCP/IP 卸载 OOB 数据中**NetBufferListInfo**数组：

<a href="" id="tcpipchecksumnetbufferlistinfo"></a>**TcpIpChecksumNetBufferListInfo**  
在卸载到微型端口驱动程序从 TCP/IP 协议的校验和任务中指定所使用的校验和信息。 当指定**TcpIpChecksumNetBufferListInfo**、 NET\_缓冲区\_列表\_信息返回[ **NDIS\_TCP\_IP\_CHECKSUM\_NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)结构 （不指向结构的指针）。 此结构包含使校验和信息可以访问作为单个 PVOID 值或为位域的联合。

<a href="" id="ipsecoffloadv1netbufferlistinfo"></a>**IPsecOffloadV1NetBufferListInfo**  
指定的 Internet 协议安全 (IPsec) 将卸载使用中的 TCP/IP 协议中为微型端口驱动程序的 IPsec 任务卸载的信息。 当指定**IPsecOffloadV1NetBufferListInfo**、 NET\_缓冲区\_列表\_信息返回[ **NDIS\_IPSEC\_将卸载\_V1\_NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info)结构。

<a href="" id="tcplargesendnetbufferlistinfo"></a>**TcpLargeSendNetBufferListInfo**  
指定卸载从 TCP/IP 协议到微型端口驱动程序的大型 TCP 数据包分段中使用的信息。 当指定**TcpLargeSendNetBufferListInfo**、 NET\_缓冲区\_列表\_信息返回[ **NDIS\_TCP\_大\_发送\_卸载\_NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)结构 （不指向结构的指针）。 此结构包含使信息可以访问作为单个 PVOID 值或为位域的联合。

<a href="" id="ieee8021qnetbufferlistinfo"></a>**Ieee8021QNetBufferListInfo**  
指定 802.1Q 的数据包的有关信息。 当指定**Ieee8021QNetBufferListInfo**、 NET\_缓冲区\_列表\_信息返回**值**隶属[ **NDIS\_NET\_缓冲区\_列表\_8021Q\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)结构。 此结构可以指定 802.1p 优先级和虚拟 LAN (VLAN) 标识符信息。 802.1p 优先级信息用于共享媒体 802 网络中建立数据包优先级。

如果微型端口驱动程序报告支持 NDIS\_封装\_IEEE\_802\_3\_P\_AND\_Q\_IN\_OOB 封装它必须插入**Ieee8021QNetBufferListInfo**数据到大量发送卸载版本 1 (LSOV1) 以及大量发送卸载版本 2 (LSOV2) 以太网数据包。

<a href="" id="tcpoffloadbytestransferred"></a>**TcpOffloadBytesTransferred**  
指定数据在 TCP 烟囱中传输的字节将卸载发送、 接收或断开连接操作的数量。

<a href="" id="tcpreceivenopush"></a>**TcpReceiveNoPush**  
指定一个布尔值，表示推送模式下的 TCP 烟囱卸载接收请求。 如果 **，则返回 TRUE**，接收请求处于非推送模式。 否则，接收请求是在推送模式下。

LSOV1，LSOV2、 校验和，以及 IPsec 卸载类型，微型端口驱动程序执行基于 OOB 数据和它将报告的卸载功能的类型的任务卸载。 例如，如果协议驱动程序需要 IPv4 数据包的 LSOV1 服务，协议驱动程序提供了每个发送请求包括中的信息**LsoV1Transmit**中的成员[ **NDIS\_TCP\_LARGE\_发送\_卸载\_NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info) OOB 数据。 请注意，协议驱动程序必须验证微型端口驱动程序支持使用指定的封装的类型、 IPv4，再在发送请求。

NDIS\_TCP\_LARGE\_发送\_卸载\_NET\_缓冲区\_列表\_结构包含的最大段大小 (MSS) 的信息。 **TcpHeaderOffset**成员指定 TCP 标头的位置，以便微型端口驱动程序不需要分析 IP 标头、 IP 选项或 IP 扩展标头。

NDIS 6.0 和更高版本支持 LSOV2 和 LSOV1 的微型端口驱动程序必须检查**类型**的成员[ **NDIS\_TCP\_大\_发送\_卸载\_NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)以确定是否使用 LSOV2 或 LSOV1 驱动程序堆栈，并必须执行相应的卸载。

为 LSOv1 之前微型端口, 驱动程序完成发送的大型的 TCP 数据包，它将已分段较小的数据包通过使用此外，驱动程序将写入它的分段数据包中发送的 TCP 有效负载字节数**TcpPayload**成员的 NDIS\_TCP\_LARGE\_发送\_卸载\_NET\_缓冲区\_列表\_信息。

如果微型端口驱动程序指定 NDIS\_封装\_IEEE\_802\_3\_P\_AND\_Q 标志及其功能，则驱动程序可能在执行任务卸载服务有关[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)包含缓冲数据中的 VLAN 标头的结构。 在接收到的数据的情况下此标志指示微型端口驱动程序将执行接收校验和计算，并将 VLAN 标头放在以太网数据包。

如果微型端口驱动程序指定 NDIS\_封装\_IEEE\_802\_3\_P\_AND\_Q\_IN\_OOB 标志中的功能，该驱动程序可以执行卸载网上\_缓冲区\_包含中的 VLAN 标头的列表结构**Ieee8021QnetBufferListInfo** OOB 数据。 在接收校验和卸载的情况下，微型端口将插入到 VLAN 标头**Ieee8021QnetBufferListInfo** OOB 数据。

 

 





