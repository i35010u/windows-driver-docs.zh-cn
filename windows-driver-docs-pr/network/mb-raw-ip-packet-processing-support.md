---
title: MB 原始 IP 数据包处理支持
description: MB 原始 IP 数据包处理支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2db313431b74218be110012185a59ff92db4cd1f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839889"
---
# <a name="mb-raw-ip-packet-processing-support"></a>MB 原始 IP 数据包处理支持


MB 微型端口驱动程序支持其发送/接收数据路径中的原始 IP 数据包帧应遵循以下准则：

### <a name="net-buffer-list-nbl-flags-for-raw-ip-packet-processing"></a>用于原始 IP 包处理 (NBL) 标志的网络缓冲区列表

-   对于 IPv4 数据包：

    [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的 **NBLFLAGS** 成员必须设置为 NDIS \_ NBL \_ 标志 \_ 为 \_ IPV4。

    **NetBufferListFrameType** \_ 网络缓冲区列表结构的 NetBufferListFrameType 成员 \_ 必须按网络字节顺序设置为 0x0800 (Ethertype IPv4) 。

-   对于 IPv6 数据包：

    网络 **NblFlags** \_ 缓冲区列表结构的 NblFlags 成员 \_ 必须设置为 NDIS \_ NBL \_ 标志 \_ 为 \_ IPV6。

    **NetBufferListFrameType** \_ 网络缓冲区列表结构的 NetBufferListFrameType 成员 \_ 必须按网络字节顺序设置为 0x86dd (Ethertype IPv6) 。

微型端口驱动程序可以使用 [**NdisSetNblFlag**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetnblflag) 宏在网络缓冲区列表中设置标志。 以下行演示了如何在网络缓冲区列表中设置 IPv4 数据包标志：

```C++
NdisSetNblFlag(pNbl, NDIS_NBL_FLAGS_IS_IPV4);
```

微型端口驱动程序可以使用 [**网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_info) 获取和设置网络缓冲区列表中的信息。 以下行演示了如何在 IPV4 数据包的网络缓冲区列表中修改 **NetBufferListFrameType** OOB：

```C++
Value = ConvertToNetworkByteOrder(0x0800);
```

```C++
NET_BUFFER_LIST_INFO(pNbl, NetBufferListFrameType) = Value;
```

### <a name="send-path-processing"></a>发送路径处理

MB 服务将在 NBL 中设置这些标志，然后将该列表传递给微型端口驱动程序以通过网络发送。 微型端口驱动程序可以验证输入 NBL 中的标志。

### <a name="receive-path-processing"></a>接收路径处理

小型端口驱动程序应在 NBL 中设置标志，然后将 NBL 传递到 MB 服务以接收数据包。

如果微型端口驱动程序在其驱动程序开发阶段实现了原始 IP 包处理，但仍启用了 DHCP 服务器欺骗 (EnableDhcp = 1) ，则微型端口驱动程序应确保：

-   在来自微型端口驱动程序的 DHCP 响应中设置的硬件地址和其长度应与 NDIS **CurrentMacAddress** **MacAddressLength** \_ 微型端口 \_ 适配器 \_ 常规属性结构中的微型端口驱动程序所指定的 CurrentMacAddress 和 MacAddressLength 成员的值匹配 \_ 。

-   事务 ID (来自微型端口驱动程序的 DHCP 响应) 的 **xid** 成员应与客户端的 dhcp 请求消息中设置的事务 id 完全匹配。

 

