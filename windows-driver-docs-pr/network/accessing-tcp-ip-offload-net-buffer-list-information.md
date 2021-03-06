---
title: 访问 TCP/IP 卸载 NET_BUFFER_LIST 信息
description: 访问 TCP/IP 卸载 NET_BUFFER_LIST 信息
keywords:
- TCP/IP 卸载 WDK 网络，带外数据
- 卸载 WDK TCP/IP 传输，带外数据 WDK TCP/IP 卸载
- OOB 数据 WDK TCP/IP 卸载
- NET_BUFFER_LIST
- 任务卸载 WDK TCP/IP 传输，带外数据
- 连接卸载 WDK TCP/IP 传输，带外数据
ms.date: 10/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: 69bbff756636ebac69f0eecc2c00cf63fd68734d
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249303"
---
# <a name="accessing-tcpip-offload-net_buffer_list-information"></a>访问 TCP/IP 卸载网络 \_ 缓冲区 \_ 列表信息

NDIS 版本6.0 和更高版本在 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)结构的 **NetBufferListInfo** 成员中提供 tcp/ip 卸载带外 (OOB) 数据，该结构指定 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer)结构的链接列表。 **NetBufferListInfo** 成员是值的数组，其中包含列表中所有网络缓冲区结构共有的信息 \_ 。

使用以下标识符和 [**NET \_ BUFFER \_ LIST \_ INFO**](/windows-hardware/drivers/ddi/nblaccessors/nf-nblaccessors-net_buffer_list_info) 宏来设置和获取 **NETBUFFERLISTINFO** 数组中的 tcp/ip 卸载 OOB 数据：

<a href="" id="tcpipchecksumnetbufferlistinfo"></a>**TcpIpChecksumNetBufferListInfo**  
指定在将校验和任务从 TCP/IP 协议卸载到微型端口驱动程序时使用的校验和信息。 指定 **TcpIpChecksumNetBufferListInfo** 时，网络 \_ 缓冲区 \_ 列表信息将 \_ 返回 [**NDIS \_ TCP \_ IP \_ 校验和 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/nblchecksum/ns-nblchecksum-ndis_tcp_ip_checksum_net_buffer_list_info) 结构， (不是指向结构) 的指针。 此结构包含一个联合，使校验和信息可以作为单个 PVOID 值或位域进行访问。

<a href="" id="ipsecoffloadv1netbufferlistinfo"></a>**IPsecOffloadV1NetBufferListInfo**  
指定在将 IPsec 任务从 TCP/IP 协议卸载到微型端口驱动程序时使用的 Internet 协议安全 (IPsec) 卸载信息。 指定 **IPsecOffloadV1NetBufferListInfo** 时，网络 \_ 缓冲区 \_ 列表 \_ 信息将返回 [**NDIS \_ IPSEC \_ 卸载 \_ V1 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info) 结构。

<a href="" id="tcplargesendnetbufferlistinfo"></a>**TcpLargeSendNetBufferListInfo**  
指定用于将大型 TCP 数据包的分段从 TCP/IP 协议卸载到微型端口驱动程序的信息。 指定 **TcpLargeSendNetBufferListInfo** 时，网络 \_ 缓冲区 \_ 列表信息将 \_ 返回 [**NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/nbllso/ns-nbllso-ndis_tcp_large_send_offload_net_buffer_list_info) 结构， (不是指向结构) 的指针。 此结构包含一个联合，使信息可以作为单个 PVOID 值或位域进行访问。

<a href="" id="ieee8021qnetbufferlistinfo"></a>**Ieee8021QNetBufferListInfo**  
指定有关数据包的 802.1 Q 信息。 指定 **Ieee8021QNetBufferListInfo** 时，NET \_ buffer \_ List \_ INFO 将返回 [**NDIS \_ 网络 \_ 缓冲区 \_ 列表 \_ 8021Q \_ info**](/windows-hardware/drivers/ddi/nbl8021q/ns-nbl8021q-ndis_net_buffer_list_8021q_info)结构的 **值** 成员。 此结构可以指定 802.1 p 优先级和虚拟 LAN (VLAN) 标识符信息。 802.1 p 优先级信息用于在共享媒体802网络中建立包优先级。

如果微型端口驱动程序报告支持 NDIS \_ 封装 \_ IEEE \_ 802 \_ 3 \_ P \_ 和 \_ \_ OOB 封装中的 Q \_ ，则它必须将 **IEEE8021QNETBUFFERLISTINFO** 数据插入到大型 send 卸载版本 1 (LSOV1) 和大量发送卸载版本 2 (LSOV2) 以太网数据包。

<a href="" id="tcpoffloadbytestransferred"></a>**TcpOffloadBytesTransferred**  
指定 TCP 烟囱卸载发送、接收或断开连接操作中传输的数据字节数。

<a href="" id="tcpreceivenopush"></a>**TcpReceiveNoPush**  
指定一个布尔值，该值表示 TCP 烟囱卸载接收请求的推送模式。 如果 **为 TRUE**，则接收请求处于非推送模式。 否则，接收请求处于推送模式。

对于 LSOV1、LSOV2、checksum 和 IPsec 卸载类型，微型端口驱动程序基于 OOB 数据的类型和它报告的卸载功能来执行任务卸载。 例如，如果某个协议驱动程序需要 IPv4 数据包的 LSOV1 服务，则该协议驱动程序提供的每个发送请求都包括 [**NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/nbllso/ns-nbllso-ndis_tcp_large_send_offload_net_buffer_list_info)OOB 数据中的 **LsoV1Transmit** 成员提供的信息。 请注意，在发出发送请求之前，协议驱动程序必须验证微型端口驱动程序是否支持具有指定封装类型的 IPv4。

NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息结构包含 (MSS) 的最大段大小。 **TcpHeaderOffset** 成员指定 TCP 标头的位置，使微型端口驱动程序不必分析 ip 标头、ip 选项或 ip 扩展标头。

支持 LSOV2 和 LSOV1 的 NDIS 6.0 和更高版本的小型小型驱动程序必须检查 [**ndis \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/nbllso/ns-nbllso-ndis_tcp_large_send_offload_net_buffer_list_info)的 **类型** 成员，以确定驱动程序堆栈是否正在使用 LSOV2 或 LSOV1，并必须执行相应的卸载。

对于 LSOv1，在微型端口驱动程序完成使用 LSO 将其分段分成较小数据包的发送之前，驱动程序会将它在分段数据包中发送的 TCP 负载字节数写入 NDIS  \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息的 TcpPayload 成员中。

如果微型端口驱动程序 \_ \_ 在其功能中指定了 NDIS 封装 IEEE \_ 802 \_ 3 \_ P \_ 和 \_ Q 标志，则驱动程序可以对包含缓冲区数据中 VLAN 标头的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构执行任务卸载服务。 对于接收的数据，此标志指示微型端口驱动程序将执行接收校验和计算，并将 VLAN 标头放入以太网数据包。

如果微型端口驱动程序 \_ \_ \_ 在其功能中指定 NDIS 封装 IEEE 802 \_ 3 \_ P \_ 和 \_ Q \_ in \_ OOB 标志，则驱动程序可以对 \_ \_ 包含 **Ieee8021QnetBufferListInfo** OOB 数据中的 VLAN 标头的网络缓冲区列表结构执行卸载。 在接收校验和卸载情况下，微型端口会将 VLAN 标头插入到 **Ieee8021QnetBufferListInfo** OOB 数据中。

 

