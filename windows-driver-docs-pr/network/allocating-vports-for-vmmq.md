---
title: 为 VMMQ 分配 VPorts
description: 出现 VMMQ 时，NDIS 会分配 VPorts。
ms.date: 02/28/2021
ms.localizationpriority: medium
ms.openlocfilehash: 393095317a309e7d3f21720ef542af7016972857
ms.sourcegitcommit: cf1f4196374c5b743448cb8d688d2223f7197d8f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/03/2021
ms.locfileid: "101751961"
---
# <a name="allocating-vports-for-vmmq"></a>为 VMMQ 分配 VPorts

当 [虚拟机 (VMMQ) ](overview-of-virtual-machine-multiple-queues.md) 功能存在于以下方式时，NDIS 会分配 VPorts。

NDIS 通过发出 [oid \_ NIC \_ 交换机 \_ CREATE \_ VPort](oid-nic-switch-create-vport.md) OID 请求，在微型端口适配器上创建非默认的 VPort。  (PF) VPort 创建 RSS 物理函数时，NDIS 会按如下所示初始化 [**ndis \_ NIC \_ 交换机 \_ VPort \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_vport_parameters) 结构：

- NDIS 将 **AttachedFunctionId** 字段设置为 **NDIS \_ PF \_ 函数 \_ ID**。

- 如果启用了 VMMQ，NDIS 会将 **NumQueuePairs** 字段设置为此 VPort 应使用的 VMMQ 队列对数。 此数字包括此 VPort 的默认 RSS 处理器。 保证处理器总数不会超过此数字。 如果禁用 VMMQ，NDIS 会将此值设置为 **1**。

- 如果启用了 VMMQ，则 **ProcessorAffinity** 字段将定义小型端口适配器为此 VPort 必须使用的潜在 RSS 处理器的位掩码。 用于填充 VPort 的间接寻址表项的网络堆栈所用的处理器是此位掩码识别的处理器的子集。 掩码将是从对 [**NdisGetRssProcessorInformation**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetrssprocessorinformation) 的调用返回的 rss 处理器的子集，并且设置的位数可能超过 VPort 请求的 rss 队列的数量。 如果禁用 VMMQ，则在设置 VPort 队列的关联时，微型端口适配器必须使用在此位掩码中指定的最小处理器数。

- NDIS 设置 NDIS \_ NIC \_ 交换机 \_ VPORT \_ PARAMS \_ NUM \_ QUEUE \_ 对 \_ CHANGED 标志，指示在创建 VPORT 后已更新 **NumQueuePairs** 成员。 启用 VMMQ 时，可以更新默认和非默认 VPorts 的队列数。 