---
title: 广告 VMMQ 功能
description: 小型端口驱动程序在小型端口适配器初始化期间注册 NIC 的 VMMQ 功能。
ms.date: 02/28/2021
ms.localizationpriority: medium
ms.openlocfilehash: dc307ae9416aba3a6955b468dcf6885aee4ba24f
ms.sourcegitcommit: cf1f4196374c5b743448cb8d688d2223f7197d8f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/03/2021
ms.locfileid: "101751964"
---
# <a name="advertising-vmmq-capabilities"></a>广告 VMMQ 功能

小型端口驱动程序在微型端口适配器初始化过程中，将 [虚拟机注册多个队列 (VMMQ) ](overview-of-virtual-machine-multiple-queues.md) 功能。

> [!NOTE]
> 如果 NIC 支持 VMMQ，则默认的 VPort 和至少一个非默认 VPort 必须支持 VMMQ。

初始化期间，微型端口驱动程序必须检查 **\* RssOnHostVPorts** INF 关键字，以确定是否应在 NIC 上启用 VMMQ 功能。 有关处理 VMMQ 的 RSS 关键字的详细信息，请参阅 [VMMQ 的标准化 INF 关键字](standardized-inf-keywords-for-vmmq.md)。 

此外，如果微型端口适配器支持创建 NIC 交换机，堆栈只能激活 NIC 上的 VMMQ。 当 **\* SriovPreferred** INF 关键字设置为 **one** ，或 **\* SriovPreferred** 设置为 **0** 且 **\* RssOrVmqPreference** 设置为 **1** 时，NDIS 可以在微型端口适配器上创建 NIC 交换机。 有关详细信息，请参阅 [适用于 sr-iov 的标准化 Inf 关键字](standardized-inf-keywords-for-sr-iov.md) 和 [VMQ 的标准化 inf 关键字](standardized-inf-keywords-for-vmq.md)。 

当微型端口驱动程序为 NIC 交换机配置参数时，它必须设置 [**NDIS \_ NIC \_ 交换机 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_parameters) 结构的字段，如下所示：

1. 将 **标头** 的 **修订** 成员设置为 **NDIS \_ NIC \_ 交换机 \_ 参数 \_ 修订版本 \_ 2**。

2. 将 **NumQueuePairsForDefaultVPort** 设置为分配给默认 VPort 的队列对数。

微型端口驱动程序通过 [**NDIS \_ NIC \_ 交换机 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities) 结构公布 NIC 的 VMMQ 功能。 微型端口驱动程序必须初始化 **NDIS \_ NIC \_ 交换机 \_ 功能** ，如下所示：

1. 将 **标头** 的 **修订** 成员设置为 **NDIS \_ NIC \_ 交换机 \_ 功能 \_ 修订版 \_ 3**。

2. 设置 **NicSwitchCapabilities** 标志，如下所示：

   - 将 NDIS \_ NIC \_ 交换机 \_ cap \_ 单一 \_ VPORT \_ 池设置为 **1** ，以指示可以在 PF 上创建非默认的 VPorts。 必须设置此标志。 

   - \_ \_ \_ \_ 为支持的非默认 VPORT 设置 ndis NIC 交换机 cap 非对称 \_ 队列 \_ 对， \_ \_ \_ \_ 以指示 NDIS 可以在每个 VPORT 上分配任意数量的 VMMQ 队列。 否则，所有非默认 VPorts 都具有与 **MaxNumQueuePairsPerNonDefaultVPort** 字段所定义的最大数目的 VMMQ 队列。 

    - \_ \_ \_ 在 pf VPORTS 上将 NDIS NIC 交换机 cap RSS 设置为 \_ \_ \_ \_ \_ **One** ，以指示 NIC 支持 VMMQ for PF VPORTS。
    
    > [!NOTE]
    > 如果未设置以下四个每个 PF VPort 标志中的任何一个，则更高级别的驱动程序将使用设置的值，这些值在设置了 PF VPorts 的 RSS 参数 (包括默认的 VPort) 时指定。 有关详细信息，请参阅 [启用、禁用和更新 VPort 上的 VMMQ](updating-vmmq-on-a-vport.md)。

    - 为 \_ \_ 每个 PF 设置 NDIS NIC 交换机 \_ cap \_ RSS \_ \_ \_ VPORT \_ 支持一个的间接寻址， \_ \_ 以指示 NIC 能够按 pf VPORT 间接表进行维护。  必须设置此标志。
    
   > [!NOTE]
   > 以下三个标记 NDIS \_ nic \_ 交换机 \_ cap \_ \_ 每个 \_ PF \_ VPORT \_ 哈希 \_ 函数 \_ 、ndis \_ nic 交换机 cap rss 每 pf 支持的哈希类型、 \_ \_ \_ \_ \_ \_ \_ \_ \_ 支持的每 \_ pf VPORT 哈希键的 ndis nic \_ 交换机 \_ cap \_ rss \_ \_ \_ \_ \_ \_ 必须全部设置为 **零** 或全部设置为 **1**。 如果它们都设置为 **零**，则软件将重新计算哈希值。 
    

    - \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ 如果 NIC 支持为每个 pf VPORT 设置不同的哈希函数，请将每个 pf 的 NDIS NIC 交换机 cap RSS VPORT 哈希函数设置为一个。

    - \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ 如果 NIC 支持在每个 pf VPORT 上设置不同的哈希类型，则将每个 pf 的 NDIS NIC 交换机 cap RSS VPORT 哈希类型设置为一个。 

    - \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ 如果 NIC 支持为每个 pf VPORT 设置不同的哈希机密密钥，请为每个 pf VPORT 哈希密钥设置 NDIS NIC 交换机 cap RSS。

    - \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ 如果 NIC 对 pf VPorts 的间接寻址表大小有限制，则将每个 PF 的 NDIS NIC 交换机 cap RSS 设置为 VPORT。 此标志强制 RSS OID 的颁发者使用每个 PF 的 VPort 间接寻址表大小，该大小等于 VPort 队列的数量，向上舍入到2的下一次幂。 此标志可以与 NDIS_NIC_SWITCH_CAPS_ASYMMETRIC_QUEUE_PAIRS_FOR_NONDEFAULT_VPORT_SUPPORTED 标志结合使用 (不同的 PF VPorts 可以具有不同数量的队列) 。 此标志阻止 VMMQ 用户执行细化队列控制。

1. 设置 **MaxNumVPorts** 以指定 VPorts 的最大数目。

1. 设置  **MaxNumQueuePairs** 以指定可分配给所有 VPorts 的最大队列对数。 这包括附加到 PF 的默认 VPort。 此数字应反映实际的硬件功能。 

1. 设置 **MaxNumQueuePairsPerNonDefaultVPort** 以指定可分配给非默认 VPort 的最大队列对数。

1. 设置 **MaxNumRssCapableNonDefaultPFVPorts** 以指定可支持 VMMQ 的非默认 PF VPorts 的最大数目。 

1. 设置 **NumberOfIndirectionTableEntriesForDefaultVPort** 以指定默认 VPort 的间接寻址表项的数目。

1. 设置 **NumberOfIndirectionTableEntriesPerNonDefaultPFVPort** 以指定每个非默认 PF VPort 的间接表项的数目。 对于所有非默认 PF VPorts，间接寻址表的大小应相同。

1. 设置 **MaxNumQueuePairsForDefaultVPort** 以指定在 NIC 交换机创建期间可以分配给默认 VPort 的最大队列对数。

播发 VMMQ 功能后，当在默认 VPort 或非默认 VPort 上调用时，NDIS 负责处理 [OID_GEN_RECEIVE_SCALE_CAPABILITIES](/windows-hardware/drivers/network/oid-gen-receive-scale-capabilities) OID。 当微型端口驱动程序返回 [**NDIS \_ 接收 \_ 缩放 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)结构中的 RSS 功能时，它不应通过任何标准 RSS 关键字 (如 **\* MaxRssProcessors**) 来约束 **NumberOfInterruptMessages** 字段。 上层驱动程序会将此数字合并为主机 CPU 分配算法。