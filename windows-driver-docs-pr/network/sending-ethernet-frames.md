---
title: 发送以太网帧
description: 发送以太网帧
ms.assetid: 9d1037b9-ef5c-4ed8-9204-5729eff2cea3
keywords:
- 以太网 WDK 网络
- 帧 WDK 网络
- 以太网帧的 TCP/IP 传输-WDK 网络
- 发送以太网帧
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f84f914bf0c40a8d1f0c146e9cdd9d3249b69b23
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841967"
---
# <a name="sending-ethernet-frames"></a>发送以太网帧





Windows TCP/IP 传输支持一组用于发送以太网帧的要求。 发起发送请求或修改过量驱动程序的发送请求的任何驱动程序（例如 MUX 中间驱动程序或筛选器驱动程序）都必须支持 TCP/IP 传输实现的要求。

**请注意**  如果驱动程序堆栈中的任何驱动程序不遵循这些要求，则基础微型端口驱动程序、MUX 中间驱动程序和筛选器驱动程序的行为可能无法预测。

 

对于以太网发送请求，驱动程序必须支持以下要求：

-   如果驱动程序发出发送请求，则驱动程序应为以太网帧分配一个[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 每个 NET\_缓冲区\_列表结构中的**NetBufferListInfo**成员必须包括特定用途所需的带外（OOB）数据。 OOB 数据适用于所有与网络\_缓冲区关联的[**net\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)\_列表结构。

-   如果驱动程序发出发送请求，则驱动程序应为以太网帧分配一个或多个 NET\_缓冲区结构，并将这些结构链接到网络\_缓冲区\_列表结构。 链接到网络\_缓冲区的每个网络\_缓冲结构\_列表结构描述单个以太网帧。 驱动程序可以在发送请求中将多个 NET\_缓冲区链接\_列表结构。 

-   与 NET\_缓冲器\_列表结构关联的所有网络\_缓冲结构必须具有相同的以太网帧类型和 IP 协议版本（IPv4 或 IPv6）。

-   与 NET\_缓冲器\_列表结构关联的所有网络\_缓冲结构必须具有相同的源和目标 MAC 地址。

-   如果驱动程序正在发送 TCP 或 UDP 帧，则与网络\_\_缓冲区关联的所有 NET\_缓冲区结构都必须与相同的 TCP 或 UDP 连接关联。
    **请注意**  受以下要求的限制，则可以拆分传输的以太网帧。 也就是说，多个内存描述符列表（MDLs）可以与发送请求中的 NET\_缓冲区结构相关联。

     

-   不要跨多个 MDLs 拆分传输以太网帧的 MAC 标头。 将虚拟 LAN （VLAN）（或优先级）标志（如果存在）视为 MAC 标头的一部分。 因此，此标志必须与 MAC 标头的其余部分位于同一 MDL。

-   如果驱动程序在网络\_缓冲区\_列表结构的网络\_缓冲区结构或网络\_缓冲区链中更改 MDL 链中的链接，则驱动程序必须先将链接还原为原始配置，然后再将 NET\_BUFFER\_列表的所有权返回到过量的驱动程序中。 但是，驱动程序不需要还原 NET\_BUFFER\_列表结构之间的链接。

 

 





