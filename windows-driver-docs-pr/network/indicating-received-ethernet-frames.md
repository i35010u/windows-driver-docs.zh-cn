---
title: 指示已接收以太网帧
description: 指示已接收以太网帧
ms.assetid: 39f35a54-1d80-4a14-b48c-2dbbfde9c86f
keywords:
- WDK 以太网网络
- 帧 WDK 网络
- 以太网帧 WDK 网络的 TCP/IP 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b69885cb4c26c31513b526eed9ee88d8070dc7d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380920"
---
# <a name="indicating-received-ethernet-frames"></a>指示已接收以太网帧





Windows TCP/IP 协议驱动程序施加了一组用于接收以太网帧的要求。 源自任何驱动程序收到的以太网帧指示或修改接收的基础指示驱动程序必须支持 TCP/IP 施加的常规要求。 这些驱动程序包括以太网微型端口驱动程序，MUX 中间驱动程序，并筛选器驱动程序。

**请注意**  驱动程序不遵循这些要求，如果过量驱动程序 （如 TCP/IP 传输、 MUX 中间驱动程序和筛选器驱动程序） 可能会行为异常。

 

源自以太网的驱动程序收到指示必须满足以下要求：

-   驱动程序必须分配[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)接收的以太网帧的结构。 每个**NET\_缓冲区\_列表**结构必须包括在中定义的带外 (OOB) 数据**NetBufferListInfo**隶属**NET\_缓冲区\_列表**特定使用所必需的。

-   驱动程序必须分配[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)为框架结构，并将其链接至[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 以太网微型端口必须分配一个**NET\_缓冲区**结构**NET\_缓冲区\_列表**结构时，该值指示接收到的数据。 此限制仅适用于以太网接收路径。 不适用于其他媒体类型，如本机 802.11 无线 LAN 接口。 或在常规的 NDIS。

-   在某些情况下，从 NDIS 6.1 [ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构可与接收的以太网帧的多个内存描述符列表 (MDLs) 相关联。 即使[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构必须包含一个**NET\_缓冲区**结构，使用多个 MDLs使驱动程序接收的数据包数据拆分为单独的缓冲区。

    例如，支持的标头数据拆分接口的以太网驱动程序通过使用一个与相关联的多个 MDLs 的链接的列表拆分接收的以太网帧[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构。 有关详细信息，请参阅[标头数据拆分](header-data-split.md)。

    出于简易性和性能原因，我们强烈建议驱动程序不支持标头数据拆分为每个使用只有一个 MDL [ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构。

    **请注意**  NDIS 6.0 适用于 Windows Vista 中每个[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构必须包含一个 MDL。

     

-   除非第一个 MDL 包含至少多少个字节作为预测先行大小为指定的 NDIS 驱动程序必须不会拆分 IP 标头、 IPv4 选项、 IPsec 标头、 IPv6 扩展标头或上层协议标头，中间接收到的以太网帧。

NDIS 协议和筛选器驱动程序必须支持拆分中的以太网帧指示如果收到此类拆分帧符合前面的列表项中定义的限制。 限制可确保协议和筛选器驱动程序都与将来的 Windows 版本兼容。

 

 





