---
title: 指示已接收以太网帧
description: 指示已接收以太网帧
keywords:
- 以太网 WDK 网络
- 帧 WDK 网络
- 以太网帧的 TCP/IP 传输-WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebf9780059dd20d5ee2688e7301d7aac3a0ce75e
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249197"
---
# <a name="indicating-received-ethernet-frames"></a>指示已接收以太网帧





Windows TCP/IP 协议驱动程序对接收以太网帧有一组要求。 任何产生以太网帧接收指示的驱动程序或修改底层驱动程序的接收指示都必须支持 TCP/IP 施加的一般要求。 这些驱动程序包括以太网微型端口驱动程序、MUX 中间驱动程序和筛选器驱动程序。

**注意**  如果驱动程序未遵循这些要求，则过量驱动程序 (如 TCP/IP 传输、MUX 中间驱动程序和筛选器驱动程序) 可能会表现出不可预测的行为。

 

发出以太网接收指示的驱动程序必须支持下列要求：

-   驱动程序必须为收到的以太网帧分配 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构。 每个 **网络 \_ 缓冲区 \_ 列表** 结构都必须包含带外 (OOB) 在特定用途需要的 **网络 \_ 缓冲区 \_ 列表** 的 **NetBufferListInfo** 成员中定义的数据。

-   驱动程序必须为帧分配 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 结构，并将其链接到 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构。 指示收到的数据时，以太网小型端口必须为 **网络 \_ 缓冲区 \_ 列表** 结构分配准确的一个 **网络 \_ 缓冲区**。 此限制仅适用于以太网接收路径。 它不适用于其他媒体类型，如本机802.11 无线 LAN 接口。 一般为或 NDIS。

-   从 NDIS 6.1 开始，在某些情况下，可以将 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 与接收的以太网帧 (MDLs) 的多个内存描述符列表相关联。 即使 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构必须包含单个 **网络 \_ 缓冲区** 结构，使用多个 MDLs，驱动程序也可以将接收的数据包数据拆分为单独的缓冲区。

    例如，支持标头的以太网驱动程序-数据拆分接口使用与单个 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 结构关联的多个 MDLs 的链接列表拆分接收到的以太网帧。 有关详细信息，请参阅 [标头-数据拆分](header-data-split.md)。

    出于简易性和性能方面的考虑，我们强烈建议不支持标头数据拆分的驱动程序对于每个 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 结构仅使用一条 MDL。

    **注意**  在适用于 Windows Vista 的 NDIS 6.0 中，每个 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 结构都必须只包含一个 MDL。

     

-   驱动程序不得将接收的以太网帧拆分为 IP 标头、IPv4 选项、IPsec 标头、IPv6 扩展标头或上层协议标头，除非第一个 MDL 至少包含与为预测先行大小指定的 NDIS 相同的字节数。

如果此类分割帧符合前面列表项中定义的限制，NDIS 协议和筛选器驱动程序必须支持在接收指示中拆分以太网帧。 这些限制确保了协议和筛选器驱动程序与未来的 Windows 版本兼容。

 

