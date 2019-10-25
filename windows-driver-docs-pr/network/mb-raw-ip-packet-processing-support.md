---
title: MB 原始 IP 数据包处理支持
description: MB 原始 IP 数据包处理支持
ms.assetid: 1c3327fa-1858-4247-9a18-b49d26e9a095
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4eb2db92922af73fdd697becb2ae4aff4efd55a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844273"
---
# <a name="mb-raw-ip-packet-processing-support"></a>MB 原始 IP 数据包处理支持


MB 微型端口驱动程序支持其发送/接收数据路径中的原始 IP 数据包帧应遵循以下准则：

### <a name="net-buffer-list-nbl-flags-for-raw-ip-packet-processing"></a>用于原始 IP 包处理的网络缓冲区列表（NBL）标志

-   对于 IPv4 数据包：

    [**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的**NblFlags**成员必须设置为 NDIS\_NBL\_标志\_\_IPV4。

    NET\_缓冲区\_列表结构的**NetBufferListFrameType**成员必须按网络字节顺序设置为0X0800 （Ethertype IPv4）。

-   对于 IPv6 数据包：

    NET\_BUFFER\_列表结构的**NblFlags**成员必须设置为 NDIS\_NBL\_标志\_\_IPV6。

    NET\_缓冲区\_列表结构的**NetBufferListFrameType**成员必须按网络字节顺序设置为0X86dd （Ethertype IPv6）。

微型端口驱动程序可以使用[**NdisSetNblFlag**](https://docs.microsoft.com/windows-hardware/drivers/network/ndissetnblflag)宏在网络缓冲区列表中设置标志。 以下行演示了如何在网络缓冲区列表中设置 IPv4 数据包标志：

```C++
NdisSetNblFlag(pNbl, NDIS_NBL_FLAGS_IS_IPV4);
```

微型端口驱动程序可以使用[**net\_BUFFER\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)来获取和设置 NET BUFFER 列表中的信息。 以下行演示了如何在 IPV4 数据包的网络缓冲区列表中修改**NetBufferListFrameType** OOB：

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

如果微型端口驱动程序在其驱动程序开发阶段实现了原始 IP 包处理，但仍启用了 DHCP 服务器欺骗（EnableDhcp = 1），则微型端口驱动程序应确保：

-   在来自微型端口驱动程序的 DHCP 响应中设置的硬件地址和其长度应与\_适配器的 NDIS\_微型端口驱动程序中的微型端口驱动程序指定的**CurrentMacAddress**和**MacAddressLength**成员的值匹配\_常规\_属性结构。

-   来自微型端口驱动程序的 DHCP 响应的事务 ID （ **xid**成员）应与客户端的 dhcp 请求消息中设置的事务 id 完全匹配。

 

 





