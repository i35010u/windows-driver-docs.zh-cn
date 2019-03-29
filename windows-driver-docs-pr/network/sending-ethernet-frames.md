---
title: 发送以太网帧
description: 发送以太网帧
ms.assetid: 9d1037b9-ef5c-4ed8-9204-5729eff2cea3
keywords:
- WDK 以太网网络
- 帧 WDK 网络
- 以太网帧 WDK 网络的 TCP/IP 传输
- 以太网帧发送
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 697f0d5e4d4f1d2531db3d0469c970e45a7fa341
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575642"
---
# <a name="sending-ethernet-frames"></a>发送以太网帧





Windows TCP/IP 传输支持发送以太网帧的一组的要求。 任何驱动程序 （例如，MUX 中间驱动程序或筛选器驱动程序），它源于发送请求或修改的过量驱动程序发送请求必须支持 TCP/IP 传输实现的要求。

**请注意**  如果驱动程序堆栈中的任何驱动程序不会遵循这些要求、 基础微型端口驱动程序、 MUX 中间驱动程序，并筛选器驱动程序可能会行为异常。

 

对于以太网发送请求，驱动程序必须支持这些要求：

-   如果驱动程序产生的发送请求，驱动程序应分配[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)为以太网帧的结构。 **NetBufferListInfo**中每个 NET 成员\_缓冲区\_列表结构必须包含所需的特定使用带外 (OOB) 数据。 OOB 数据应用于的所有[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)与网络相关联的结构\_缓冲区\_列表结构。

-   如果驱动程序产生的发送请求，该驱动程序应分配一个或多个 NET\_缓冲区为以太网帧的结构并将这些结构链接到 NET\_缓冲区\_列表结构。 每个 NET\_缓冲区结构链接到 NET\_缓冲区\_列表结构描述一个以太网帧。 该驱动程序可以链接多个 NET\_缓冲区\_列表结构中的发送请求。 

-   所有的 NET\_与网络相关联的缓冲区结构\_缓冲区\_列表结构必须具有相同的以太网帧类型和 IP 协议版本 （IPv4 或 IPv6）。

-   所有的 NET\_与网络相关联的缓冲区结构\_缓冲区\_列表结构必须具有相同的源和目标 MAC 地址。

-   如果驱动程序发送 TCP 或 UDP 帧，所有 NET\_与网络相关联的缓冲区结构\_缓冲区\_列表结构必须与同一 TCP 或 UDP 连接相关联。
    **请注意**  可以遵循以下要求，拆分发送以太网帧。 多个内存描述符列表 (MDLs) 可以与网络相关联，即\_缓冲区的发送请求中的结构。

     

-   跨多个 MDLs 不拆分传输以太网帧的 MAC 标头。 如果存在，将虚拟 LAN (VLAN) （或优先级） 的标志，作为 MAC 报头的一部分。 因此，此标志必须为相同 MDL MAC 标头的其余部分。

-   如果驱动程序将更改在 NET MDL 链中的链接\_缓冲区结构或 NET\_缓冲区链中 NET\_缓冲区\_列表结构的驱动程序必须还原到之前的原始配置链接返回的 NET 所有权\_缓冲区\_到基础驱动程序的列表。 但是，驱动程序不需要恢复网络之间的链接\_缓冲区\_列表结构。

 

 





