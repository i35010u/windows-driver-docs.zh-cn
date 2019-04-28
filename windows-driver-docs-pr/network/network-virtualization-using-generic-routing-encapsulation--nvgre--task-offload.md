---
title: NVGRE 任务卸载
description: 本部分介绍使用通用路由封装 (NVGRE) 任务卸载的网络虚拟化
ms.assetid: D1BE5659-4491-411B-9D32-9CB7A141A240
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61ff1dc27865727c148b2450d29d31f288135aff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348263"
---
# <a name="network-virtualization-using-generic-routing-encapsulation-nvgre-task-offload"></a>使用通用路由封装 (NVGRE) 任务卸载实现网络虚拟化

HYPER-V 网络虚拟化支持网络虚拟化使用通用路由封装 (NVGRE) 作为机制来虚拟化 IP 地址。 在 NVGRE 中，虚拟机的数据包被封装在另一个数据包。 此新，NVGRE 格式数据包的标头具有适当的源和目标提供程序区域 (PA) IP 地址。 此外，它有 24 位虚拟子网 ID (VSID)，它存储在 GRE 报头中的新的数据包。

下图显示了 GRE 封装的数据包。 在网络上 NVGRE 封装的数据包，如下所示 IP over 以太网数据包，只不过外部 IP 标头的有效负载是 GRE 封装 IP 数据包 （包括以太网标头）。

![原始数据包和 gre 封装数据包之间的比较。 两个都包含 mac （gre 包含内部 mac），ip 标头 （gre 包含内部 ip 标头），tcp 标头和 tcp 用户数据。 此外，使用 gre 封装的数据包包含外部 mac、 外部 ip 标头和 gre。](images/nvgre.png)

NDIS 6.30 （适用于 Windows Server 2012 和更高版本） 引入了 NVGRE 任务卸载，这使得可以使用 NVGRE 格式的数据包，其中：

-   大量发送卸载 (LSO)
-   虚拟机队列 (VMQ)
-   传输 （德克萨斯州） 校验和卸载 （IPv4、 TCP、 UDP）
-   接收 (Rx) 校验和卸载 （IPv4、 TCP、 UDP）

**请注意**  可能协议驱动程序以卸载"混合的模式"数据包，这意味着的数据包内部和外部 IP 标头版本有所不同。 例如，一个数据包可以作为 IPv6 的外部 IP 标头和与 IPv4 的内部 IP 标头。

 

**请注意**  还有可能协议驱动程序来卸载没有内部 TCP 或 UDP 标头的 NVGRE 格式的数据包。 例如，IP 数据包可能是 Internet 控制消息协议 (ICMP) 数据包的内部负载。

 

有关 NVGRE 的详细信息，请参阅以下 Internet 草案：

-   [NVGRE:使用通用路由封装网络虚拟化](http://ietfreport.isoc.org/idref/draft-sridharan-virtualization-nvgre/)

NVGRE 为基础上通用路由封装 (GRE)。 GRE 有关详细信息，请参阅以下资源：

-   [RFC 2784:通用路由封装 (GRE)](http://tools.ietf.org/html/rfc2784)
-   [RFC 2890:键和序列号 GRE 扩展](http://tools.ietf.org/html/rfc2890)

本部分包括：

-   [使用通用路由封装 (NVGRE) 任务卸载的网络虚拟化概述](overview-of-network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)
-   [在大量发送卸载 (LSO) 中支持 NVGRE](supporting-nvgre-in-large-send-offload--lso-.md)
-   [NVGRE 支持在校验和卸载](supporting-nvgre-in-checksum-offload.md)
-   [支持 NVGRE 在 RSS 和 VMQ 接收任务卸载](supporting-nvgre-in-rss-and-vmq-receive-task-offloads.md)
-   [查找的传输标头封装的数据包中的接收路径](locating-the-transport-header-for-encapsulaged-packets-in-the-receive-path.md)
-   [确定网络适配器的 NVGRE 任务卸载功能](determining-the-nvgre-task-offload-capabilities-of-a-network-adapter.md)
-   [查询和更改 NVGRE 任务卸载状态](querying-and-changing-nvgre-task-offload-state.md)
-   [NVGRE 任务卸载的标准化的 INF 关键字](standardized-inf-keywords-for-nvgre-task-offload.md)

## <a name="related-topics"></a>相关主题


[将校验和任务](offloading-checksum-tasks.md)

[卸载大型 TCP 数据包的分段](offloading-the-segmentation-of-large-tcp-packets.md)

[TCP/IP 任务卸载](task-offload.md)

 

 






