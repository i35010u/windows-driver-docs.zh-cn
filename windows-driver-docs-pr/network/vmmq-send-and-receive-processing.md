---
title: VMMQ 发送和接收处理
description: VMMQ 发送和接收处理
ms.date: 02/28/2021
ms.localizationpriority: medium
ms.openlocfilehash: dd58119012589fc0d2bb2d37398ff5a25d655e86
ms.sourcegitcommit: cf1f4196374c5b743448cb8d688d2223f7197d8f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/03/2021
ms.locfileid: "101751963"
---
# <a name="vmmq-send-and-receive-processing"></a>VMMQ 发送和接收处理

[虚拟机多个队列 (VMMQ) ](overview-of-virtual-machine-multiple-queues.md) 使用 RSS 处理为物理函数 [虚拟端口](virtual-ports--vports-.md) (PF VPorts) 高效地分发网络流量。 有关 [单根 i/o 虚拟化 (sr-iov) ](overview-of-single-root-i-o-virtualization--sr-iov-.md) 接口及其组件的详细信息，请参阅 [sr-iov 体系结构](sr-iov-architecture.md)。

下图显示了 VMMQ 接口中的网络数据包接收路径。

![用 vmmq 演示网络数据包数据路径的图示](images/vmmq-architecture.png)

当数据包到达支持 VMMQ NIC 的 NIC 时，在接收路径上：

1. 匹配目标 MAC 地址以查找目标 VPort。 

1. 使用 VPort 的 [rss 参数](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters) (机密密钥、哈希函数和哈希类型) 来计算数据包的 RSS 哈希值。 

1. 使用哈希值为与 VPort 关联的间接寻址表编制索引。 间接表中的值用于将接收的数据分配给处理器。

1. 中断目标处理器并向主机网络堆栈指示收到的数据包。 

当指示收到的 NBL 时，微型端口适配器将) 字段的带外 (OOB 设置为合适的值。

在传输路径上，NIC 必须使用数据包 (中的 RSS 哈希值（如果存在）作为 VPort 的 RSS 间接表的索引) 。 NIC 使用此间接寻址表值来确定处理数据包的传输完成中断和 Dpc 的处理器。

如果 NIC 无法计算收到的数据包的 RSS 哈希值，或者 RSS 哈希值不在传输数据包中，则应使用 VPort 的默认 RSS 处理器作为目标 RSS 处理器。 VPort 的默认 RSS 处理器将在 VPort 的 RSS 参数中指定。 有关详细信息，请参阅 [启用、禁用和更新 VPort 上的 VMMQ](updating-vmmq-on-a-vport.md)。

主机网络堆栈可在运行时动态更新 VPort 的 RSS 参数。 NIC 应响应 VPort 的 RSS 参数中的更改，并且 VPort 的流量中断最小。


