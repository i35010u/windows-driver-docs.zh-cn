---
title: 访问 TCP/IP 卸载 NET_BUFFER_LIST 信息
description: 访问 TCP/IP 卸载 NET_BUFFER_LIST 信息
ms.assetid: 555c9533-ab3f-43f0-9139-b1de33a6b1a7
keywords:
- TCP/IP 卸载 WDK 网络，带外数据
- 卸载 WDK TCP/IP 传输，带外数据 WDK TCP/IP 卸载
- OOB 数据 WDK TCP/IP 卸载
- NET_BUFFER_LIST
- 任务卸载 WDK TCP/IP 传输，带外数据
- 连接卸载 WDK TCP/IP 传输，带外数据
ms.date: 10/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4bb4574033e864b4a2bff593f087e32a89b63f5f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838251"
---
# <a name="accessing-tcpip-offload-net_buffer_list-information"></a>访问 TCP/IP 卸载\_缓冲区\_列表信息

NDIS 版本6.0 和更高版本提供了[**net\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的**NetBufferListInfo**成员提供的 tcp/ip 卸载带外（OOB）数据，它指定了[**网络\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的链接列表。 **NetBufferListInfo**成员是值的数组，其中包含列表中所有 NET\_缓冲区结构共有的信息。

将以下标识符与[**NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)宏一起使用，以在**NetBufferListInfo**数组中设置和获取 tcp/ip 卸载 OOB 数据：

<a href="" id="tcpipchecksumnetbufferlistinfo"></a>**TcpIpChecksumNetBufferListInfo**  
指定在将校验和任务从 TCP/IP 协议卸载到微型端口驱动程序时使用的校验和信息。 指定**TcpIpChecksumNetBufferListInfo**时，NET\_BUFFER\_列表\_信息返回[ **\_TCP\_IP\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)\_\_\_\_（而不是指向结构的指针）。 此结构包含一个联合，使校验和信息可以作为单个 PVOID 值或位域进行访问。

<a href="" id="ipsecoffloadv1netbufferlistinfo"></a>**IPsecOffloadV1NetBufferListInfo**  
指定在将 IPsec 任务从 TCP/IP 协议卸载到微型端口驱动程序时使用的 Internet 协议安全（IPsec）卸载信息。 指定**IPsecOffloadV1NetBufferListInfo**时，NET\_BUFFER\_列表\_信息返回[ **\_IPSEC\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info)\_\_\_\_\_构造.

<a href="" id="tcplargesendnetbufferlistinfo"></a>**TcpLargeSendNetBufferListInfo**  
指定用于将大型 TCP 数据包的分段从 TCP/IP 协议卸载到微型端口驱动程序的信息。 指定**TcpLargeSendNetBufferListInfo**时，NET\_BUFFER\_列表\_信息返回[**NDIS\_TCP\_\_NET\_\_\_\_\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)结构（不是指向结构的指针）。 此结构包含一个联合，使信息可以作为单个 PVOID 值或位域进行访问。

<a href="" id="ieee8021qnetbufferlistinfo"></a>**Ieee8021QNetBufferListInfo**  
指定有关数据包的 802.1 Q 信息。 指定**Ieee8021QNetBufferListInfo**时，NET\_BUFFER\_列表\_信息返回[**NDIS\_NET\_\_\_\_8021Q INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)结构的**值**成员。 此结构可以指定 802.1 p 优先级和虚拟 LAN （VLAN）标识符信息。 802.1 p 优先级信息用于在共享媒体802网络中建立包优先级。

如果微型端口驱动程序报告支持 NDIS\_封装\_IEEE\_802\_3\_P\_和\_，它必须将**Ieee8021QNetBufferListInfo**数据插入大型发送卸载版本1（LSOV1）和大型发送卸载版本2（LSOV2）以太网包。

<a href="" id="tcpoffloadbytestransferred"></a>**TcpOffloadBytesTransferred**  
指定 TCP 烟囱卸载发送、接收或断开连接操作中传输的数据字节数。

<a href="" id="tcpreceivenopush"></a>**TcpReceiveNoPush**  
指定一个布尔值，该值表示 TCP 烟囱卸载接收请求的推送模式。 如果**为 TRUE**，则接收请求处于非推送模式。 否则，接收请求处于推送模式。

对于 LSOV1、LSOV2、checksum 和 IPsec 卸载类型，微型端口驱动程序基于 OOB 数据的类型和它报告的卸载功能来执行任务卸载。 例如，如果某个协议驱动程序需要 IPv4 数据包的 LSOV1 服务，则该协议驱动程序提供的每个发送请求都包含来自 [**NDIS\_TCP\_大型\_发送 @no__t_ 的信息。6_ 卸载\_NET\_BUFFER\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)OOB 数据。 请注意，在发出发送请求之前，协议驱动程序必须验证微型端口驱动程序是否支持具有指定封装类型的 IPv4。

NDIS\_TCP\_大规模\_发送\_卸载\_NET\_BUFFER\_\_INFO 结构包含最大段大小（MSS）。 **TcpHeaderOffset**成员指定 TCP 标头的位置，使微型端口驱动程序不必分析 ip 标头、ip 选项或 ip 扩展标头。

支持 LSOV2 和**LSOV1 的 ndis** 6.0 和更高版本的小型小型驱动程序必须检查[**ndis\_TCP\_大型\_发送\_卸载\_NET\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)驱动程序堆栈是否正在使用 LSOV2 或 LSOV1，并必须执行相应的卸载。

对于 LSOv1，在微型端口驱动程序完成使用 LSO 将其分段分成较小数据包的发送之前，驱动程序会将它在分段数据包中发送的 TCP 负载字节数写入 NDIS @no__t_1_ TCP\_大型\_发送\_卸载\_NET\_BUFFER\_LIST\_INFO。

如果微型端口驱动程序在其功能中指定 NDIS\_封装\_IEEE\_802\_3\_P\_和\_Q 标志，则驱动程序可以为 NET\_缓冲区执行任务卸载服务[ **\_列出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)缓冲区数据中包含 VLAN 标头的结构。 对于接收的数据，此标志指示微型端口驱动程序将执行接收校验和计算，并将 VLAN 标头放入以太网数据包。

如果微型端口驱动程序指定了 NDIS\_封装\_IEEE\_802\_3\_P\_并在其功能中\_的 OOB 标志\_，驱动程序可以在包含**Ieee8021QnetBufferListInfo** OOB 数据的 VLAN 标头的 NET\_BUFFER\_列表结构上执行卸载。 在接收校验和卸载情况下，微型端口会将 VLAN 标头插入到**Ieee8021QnetBufferListInfo** OOB 数据中。

 

 





