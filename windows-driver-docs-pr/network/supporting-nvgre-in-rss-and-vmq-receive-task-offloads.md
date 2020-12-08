---
title: 在 RSS 和 VMQ 接收任务卸载中支持 NVGRE
description: 本部分介绍 RSS 和 VMQ 接收任务卸载中的支持 NVGRE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcec3b4c281ff41ad8709c93477eb5509eb365c5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841163"
---
# <a name="supporting-nvgre-in-rss-and-vmq-receive-task-offloads"></a>在 RSS 和 VMQ 接收任务卸载中支持 NVGRE


 (Windows Server 2012) NDIS 6.30 介绍了 [使用通用路由封装的网络虚拟化 (NVGRE) ](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)。 执行 [接收方缩放](receive-scaling.md) (RSS 的 NDIS 微型端口驱动程序和 nic) 和 [虚拟机队列 (VMQ) ](virtual-machine-queue--vmq-.md) 接收任务卸载应以支持 NVGRE 的方式进行。

**注意**  本页假设你熟悉如何 [分担大 TCP 数据包的分段](offloading-the-segmentation-of-large-tcp-packets.md)。

 

如果微型端口驱动程序支持封装包的 RSS 和 VMQ，则必须在 [**NDIS \_ 封装的 \_ 数据包 \_ 任务 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)结构的 **RssSupported** 和 **VmqSupported** 成员中公布这些功能。 如果微型端口播发了这些功能，接收到了 [oid \_ TCP \_ 卸载 \_ 参数](./oid-tcp-offload-parameters.md) OID 请求，并成功了 oid，则 NIC 必须对播发的封装的数据包类型执行 RSS 和 VMQ。

对于能够分析的受支持的封装数据包，NIC 必须在传输 (内部) IP 标头和内部 MAC 标头上的 VMQ 的传输负载中的 TCP 或 UDP 标头上执行 RSS。

若要执行 RSS 和 VMQ，NIC 必须转到封装包的传输 (内部) IP 标头，如在 [接收路径中查找封装的数据包的传输标头](locating-the-transport-header-for-encapsulaged-packets-in-the-receive-path.md) 和检查协议号。 如果 NIC 收到的数据包使用 NIC 可以分析的协议，则 NIC 应：

-   通过对传输 (内部) IP 标头和 TCP 或 UDP 标头执行4元组哈希来执行 RSS。
    -   对于微型端口无法分析其协议的封装数据包，NIC 应该对隧道中的源地址和目标地址字段执行2元组哈希 (外部) IP 标头。
    -   对于在传输 (内部) IP 标头之后不包含 TCP 或 UDP 标头的封装数据包，NIC 应该对隧道中的源地址和目标地址字段执行2元组哈希， (外部) IP 标头。
-   使用封装的数据包中的以太网标头执行 VMQ。 对于封装的数据包) 内不包含以太网标头 (的封装数据包，应使用最外面的以太网标头来执行 VMQ。

 

