---
title: 关于使用通用路由封装 (NVGRE) 实现网络虚拟化
description: 本部分介绍使用通用路由封装 (NVGRE) 任务卸载的网络虚拟化
ms.assetid: D1BE5659-4491-411B-9D32-9CB7A141A240
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16e51e293484a66e72c8f408a9b6abc47c429c80
ms.sourcegitcommit: b75e9940d49410e2b952e96f325df67a039cd571
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/21/2020
ms.locfileid: "92337024"
---
# <a name="about-network-virtualization-using-generic-routing-encapsulation-nvgre"></a>关于使用通用路由封装 (NVGRE) 实现网络虚拟化

Hyper-v 网络虚拟化支持使用通用路由封装 (NVGRE) 作为虚拟化 IP 地址的机制的网络虚拟化。 在 NVGRE 中，虚拟机的数据包封装在另一个数据包中。 此新的、NVGRE 格式的数据包的标头具有适当的源和目标提供者区域 (PA) IP 地址。 此外，它还具有一个24位虚拟子网 ID (VSID) ，它存储在新数据包的 GRE 标头中。

下图显示了一个 GRE 封装的数据包。 在网络上，NVGRE 封装的数据包类似于 IP over IP 数据包，只不过外部 IP 标头的负载是 GRE 封装的 IP 数据包 (包括以太网标头) 。

![原始数据包与包含 gre 封装的数据包之间的比较。 二者都包含 mac (gre 包含内部 mac) 、ip 标头 (gre 包含内部 ip 标头) 、tcp 标头和 tcp 用户数据。 此外，包含 gre 封装的数据包包含外部 mac、外部 ip 标头和 gre。](images/nvgre.png)

Windows Server 2012 和更高版本中提供的 NDIS 6.30 () 引入 NVGRE 任务卸载，使你能够在以下情况下使用 NVGRE 格式的数据包：

- 大量发送卸载 (LSO)
- 虚拟机队列 (VMQ)
- 传输 (Tx) 校验和卸载 (IPv4、TCP、UDP) 
- 接收 (Rx) 校验和卸载 (IPv4、TCP、UDP) 

**注意**  协议驱动程序可以卸载 "混合模式" 数据包，这意味着内部和外部 IP 标头版本不同的数据包。 例如，数据包可以将外部 IP 标头作为 IPv6，将内部 IP 标头作为 IPv4。

**注意**  协议驱动程序还可以卸载没有内部 TCP 或 UDP 标头的 NVGRE 格式的数据包。 例如，IP 数据包的内部有效负载为 Internet 控制消息协议 (ICMP) 数据包。

有关 NVGRE 的详细信息，请参阅以下 Internet 草案：

- [NVGRE：使用通用路由封装的网络虚拟化](https://tools.ietf.org/html/rfc7637)

NVGRE 基于 (GRE) 的通用路由封装。 有关 GRE 的详细信息，请参阅以下资源：

- [RFC 2784：泛型路由封装 (GRE) ](https://tools.ietf.org/html/rfc2784)
- [RFC 2890： GRE 的密钥和序列号扩展](https://tools.ietf.org/html/rfc2890)

本节包括：

- [有关使用通用路由封装 (NVGRE) 任务卸载实现网络虚拟化的概述](overview-of-network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)
- [在大规模发送卸载 (LSO) 中支持 NVGRE](supporting-nvgre-in-large-send-offload--lso-.md)
- [在校验和卸载中支持 NVGRE](supporting-nvgre-in-checksum-offload.md)
- [在 RSS 和 VMQ 接收任务卸载中支持 NVGRE](supporting-nvgre-in-rss-and-vmq-receive-task-offloads.md)
- [在接收路径中查找已封装数据包的传输标头](locating-the-transport-header-for-encapsulaged-packets-in-the-receive-path.md)
- [确定网络适配器的 NVGRE 任务卸载功能](determining-the-nvgre-task-offload-capabilities-of-a-network-adapter.md)
- [查询和更改 NVGRE 任务卸载状态](querying-and-changing-nvgre-task-offload-state.md)
- [NVGRE 任务卸载的标准化 INF 关键字](standardized-inf-keywords-for-nvgre-task-offload.md)

## <a name="related-topics"></a>相关主题

[卸载校验和任务](offloading-checksum-tasks.md)

[卸载大型 TCP 数据包的段](offloading-the-segmentation-of-large-tcp-packets.md)

[TCP/IP 任务卸载](task-offload.md)
