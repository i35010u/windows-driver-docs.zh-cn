---
title: 指示已接收以太网帧
description: 指示已接收以太网帧
ms.assetid: 39f35a54-1d80-4a14-b48c-2dbbfde9c86f
keywords:
- 以太网 WDK 网络
- 帧 WDK 网络
- 以太网帧的 TCP/IP 传输-WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9d017300abc4bfb6bcc4309e7e307bfae9e9a53
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824617"
---
# <a name="indicating-received-ethernet-frames"></a>指示已接收以太网帧





Windows TCP/IP 协议驱动程序对接收以太网帧有一组要求。 任何产生以太网帧接收指示的驱动程序或修改底层驱动程序的接收指示都必须支持 TCP/IP 施加的一般要求。 这些驱动程序包括以太网微型端口驱动程序、MUX 中间驱动程序和筛选器驱动程序。

**请注意**  如果驱动程序未遵循这些要求，则过量驱动程序（如 tcp/ip 传输、MUX 中间驱动程序和筛选器驱动程序）的行为可能无法预测。

 

发出以太网接收指示的驱动程序必须支持下列要求：

-   驱动程序必须为收到的以太网帧分配一个[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 每个**NET\_缓冲区\_列表**结构都必须包含在特定用途所需的**NET\_缓冲区\_列表**的**NetBufferListInfo**成员中定义的带外（OOB）数据。

-   驱动程序必须为帧分配[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构，并将其链接到[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 指示收到的数据时，以太网小型端口必须为**网络\_缓冲区**分配准确的**网络\_缓冲区**结构\_列表结构。 此限制仅适用于以太网接收路径。 它不适用于其他媒体类型，如本机802.11 无线 LAN 接口。 一般为或 NDIS。

-   从 NDIS 6.1 开始，在某些情况下， [**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构可与收到的以太网帧的多个内存描述符列表（MDLs）相关联。 即使[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构必须包含单个**网络\_缓冲区**结构，使用多个 MDLs 时，驱动程序也可使该驱动程序将接收的数据包数据拆分为单独的缓冲区。

    例如，支持标头-数据拆分接口的以太网驱动程序通过使用与单个[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构关联的多个 MDLs 的链接列表拆分接收到的以太网帧。 有关详细信息，请参阅[标头-数据拆分](header-data-split.md)。

    出于简易性和性能方面的考虑，我们强烈建议不支持标头数据拆分的驱动程序只对每个[**NET\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构使用一个 MDL。

    **请注意**  在 NDIS 6.0 For Windows Vista 中，每个[**网络\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构必须只包含一个 MDL。

     

-   驱动程序不得将接收的以太网帧拆分为 IP 标头、IPv4 选项、IPsec 标头、IPv6 扩展标头或上层协议标头，除非第一个 MDL 至少包含与为预测先行大小指定的 NDIS 相同的字节数。

如果此类分割帧符合前面列表项中定义的限制，NDIS 协议和筛选器驱动程序必须支持在接收指示中拆分以太网帧。 这些限制确保了协议和筛选器驱动程序与未来的 Windows 版本兼容。

 

 





