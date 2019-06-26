---
title: MB 原始 IP 数据包处理支持
description: MB 原始 IP 数据包处理支持
ms.assetid: 1c3327fa-1858-4247-9a18-b49d26e9a095
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0bbe7a81c027247557cd66b9d749e4ccae03413
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374021"
---
# <a name="mb-raw-ip-packet-processing-support"></a>MB 原始 IP 数据包处理支持


支持在其发送/接收的数据路径中的原始 IP 数据包帧的 MB 微型端口驱动程序应遵守以下准则：

### <a name="net-buffer-list-nbl-flags-for-raw-ip-packet-processing"></a>原始 IP 数据包处理的网络缓冲区列表 (NBL) 标志

-   为 IPv4 数据包：

    **NblFlags**的成员[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构必须设置为 NDIS\_NBL\_标志\_IS\_IPV4。

    **NetBufferListFrameType** NET 成员\_缓冲区\_列表结构必须设置为以网络字节顺序 0x0800 (Ethertype IPv4)。

-   IPv6 数据包：

    **NblFlags** NET 成员\_缓冲区\_列表结构必须设置为 NDIS\_NBL\_标志\_IS\_IPV6。

    **NetBufferListFrameType** NET 成员\_缓冲区\_列表结构必须设置为以网络字节顺序 0x86dd (Ethertype IPv6)。

微型端口驱动程序可以使用[ **NdisSetNblFlag** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndissetnblflag)宏在 net 缓冲区列表中设置标志。 下面一行演示了如何在 net 缓冲区列表中设置 IPv4 数据包标志：

```C++
NdisSetNblFlag(pNbl, NDIS_NBL_FLAGS_IS_IPV4);
```

微型端口驱动程序可以使用[ **NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)获取和设置 net 缓冲区列表中的信息。 下面一行演示了如何修改**NetBufferListFrameType** OOB IPV4 数据包的网络缓冲区列表中：

```C++
Value = ConvertToNetworkByteOrder(0x0800);
```

```C++
NET_BUFFER_LIST_INFO(pNbl, NetBufferListFrameType) = Value;
```

### <a name="send-path-processing"></a>路径处理和发送

将列表传递给要在网络上发送的微型端口驱动程序之前，MB 服务将在 NBL 中设置这些标志。 微型端口驱动程序可以验证输入 NBL 中的标志。

### <a name="receive-path-processing"></a>接收路径处理

然后再将 NBL 传递到 MB 服务收到的数据包，微型端口驱动程序应在 NBL 设置标志。

如果您的微型端口驱动程序实现原始 IP 数据包处理其驱动程序开发阶段，但仍启用了 DHCP 服务器欺骗 (EnableDhcp = 1)，您的微型端口驱动程序应确保以下：

-   硬件地址和微型端口驱动程序从 DHCP 响应中设置其长度的值应匹配**CurrentMacAddress**并**MacAddressLength**微型端口驱动程序中指定的成员NDIS\_微型端口\_适配器\_常规\_属性结构。

-   事务 ID ( **xid**成员) 的 DHCP 响应从微型端口驱动程序，应匹配完全从客户端设置 DHCP 请求消息中的事务 ID。

 

 





