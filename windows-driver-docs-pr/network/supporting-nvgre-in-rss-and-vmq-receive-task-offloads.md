---
title: 在 RSS 和 VMQ 接收任务卸载中支持 NVGRE
description: 本部分介绍 RSS 和 VMQ 接收任务卸载中的支持 NVGRE
ms.assetid: 42660D55-31C0-4101-9EA1-159EBB76B019
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fd2f3a9f274b1c06785dff637a3c2f2f71f23f4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841790"
---
# <a name="supporting-nvgre-in-rss-and-vmq-receive-task-offloads"></a>在 RSS 和 VMQ 接收任务卸载中支持 NVGRE


NDIS 6.30 （Windows Server 2012）[使用通用路由封装（NVGRE）引入网络虚拟化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)。 执行[接收方缩放](receive-scaling.md)（RSS）和[虚拟机队列（VMQ）](virtual-machine-queue--vmq-.md)接收任务卸载的 NDIS 微型端口驱动程序和 NIC 应该以支持 NVGRE 的方式执行此操作。

**请注意**  本页假设你熟悉了如何[分担大 TCP 数据包的分段](offloading-the-segmentation-of-large-tcp-packets.md)。

 

如果微型端口驱动程序支持封装包的 RSS 和 VMQ，则它必须在[ **\_数据包\_任务\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)结构的**RssSupported**和**VmqSupported**\_成员中公布这些功能。 如果微型端口播发了这些功能，则接收到[\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)OID 请求，并成功执行 OID，NIC 必须在播发的封装的数据包类型上执行 RSS 和 VMQ。

对于能够分析的支持的封装的数据包，NIC 必须在传输（内部） IP 标头的负载和内部 MAC 标头上的 VMQ 的 TCP 或 UDP 标头上执行 RSS。

若要执行 RSS 和 VMQ，NIC 必须到达封装的数据包的传输（内部） IP 标头，如在[接收路径中查找封装的数据包的传输标头](locating-the-transport-header-for-encapsulaged-packets-in-the-receive-path.md)和检查协议号。 如果 NIC 收到的数据包使用 NIC 可以分析的协议，则 NIC 应：

-   通过对传输（内部） IP 标头和 TCP 或 UDP 标头执行4元组哈希来执行 RSS。
    -   对于微型端口无法分析其协议的封装数据包，NIC 应该对隧道（外部） IP 标头中的源地址和目标地址字段执行2元组哈希。
    -   对于在传输（内部） IP 标头之后不包含 TCP 或 UDP 标头的封装数据包，NIC 应该对隧道（外部） IP 标头中的源地址和目标地址字段执行2元组哈希。
-   使用封装的数据包中的以太网标头执行 VMQ。 对于不包含以太网标头的封装包（在封装的数据包中），应使用最外面的以太网标头来执行 VMQ。

 

 





