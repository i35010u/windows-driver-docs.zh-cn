---
title: NetAdapterCx 接收方缩放 (RSS)
description: NetAdapterCx 接收方缩放 (RSS)
ms.assetid: 85A819E2-6352-4DE9-9689-3DCEB9B0AAD8
keywords:
- WDF 网络适配器类扩展接收方缩放、NetAdapterCx 接收方缩放、NetAdapterCx RSS、Get-netadapter RSS
ms.date: 07/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: bf77d90fc0aaebf7177aaa5a2624500b5a29b621
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214081"
---
# <a name="netadaptercx-receive-side-scaling-rss"></a>NetAdapterCx 接收方缩放 (RSS)

接收方缩放 (RSS) 是一种网络驱动程序技术，可用于在多处理器系统中跨多个 Cpu 高效地分发网络接收处理。 RSS 可通过利用系统中的所有可用处理器并动态重新平衡 CPU 工作负荷，提高系统性能并提高网络的可伸缩性。 

本主题重点介绍 NetAdapterCx 客户端驱动程序的 RSS，并假设了解 RSS 概念和术语。 有关常规 RSS 的详细信息，包括在不同硬件方案中阐释 RSS 的图表，请参阅 [接收方缩放](../network/receive-side-scaling-version-2-rssv2-.md)。

## <a name="overview-of-rss-in-netadaptercx"></a>NetAdapterCx 中的 RSS 概述

NetAdapterCx 中的 RSS 重点介绍了易于配置、支持和禁用的简单性，以及处理器到中断的复杂性。 支持 RSS 的 NIC 的客户端驱动程序只需满足三个条件即可在 NetAdapterCx 中支持 RSS：

1. 驱动程序必须在启动网络适配器时，但在调用 [**NetAdapterStart**](/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)之前设置 RSS 功能。 这包括实现四个 RSS 回调并在 RSS 功能结构中注册它们。
2. 必须创建驱动程序的数据路径队列，并准备好接受请求。
3. 驱动程序必须处于 *D0* 电源状态。

NetAdapterCx 中的 RSS 设计保证系统在 [启动序列](power-up-sequence-for-a-netadaptercx-client-driver.md)的最末尾之前，不会调用客户端的 rss 回调并启用 rss。 客户端无需管理间接寻址表移动请求或处理其他 RSS 事件，直到它们所需的一切就绪。 

稍后，当卸载驱动程序时，NetAdapterCx 将不会在关闭 [序列](power-down-sequence-for-a-netadaptercx-client-driver.md)期间销毁数据路径队列后调用 RSS 回调。 由于在关机过程中，数据路径队列被分解为第一步，这意味着客户端无需在关机时处理任何其他阶段的可能 RSS 事件。

## <a name="setting-rss-capabilities"></a>设置 RSS 功能

若要开始在 NetAdapterCx 中开始处理 RSS，请遵循以下步骤：

1. 启动网络适配器时，请使用 [NET_ADAPTER_RECEIVE_SCALING_CAPABILITIES](/windows-hardware/drivers/ddi/netreceivescaling/ns-netreceivescaling-_net_adapter_receive_scaling_capabilities) 结构告诉系统硬件的 RSS 功能和约束。
2. 通过调用 [NET_ADAPTER_RECEIVE_SCALING_CAPABILITIES_INIT](/windows-hardware/drivers/ddi/netreceivescaling/nf-netreceivescaling-net_adapter_receive_scaling_capabilities_init)初始化功能结构。 
3. 初始化 RSS 功能结构时，请设置结构的 RSS 回叫成员，为这些回调注册实现：
    1. *[EvtNetAdapterReceiveScalingEnable](/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_enable)*
    2. *[EvtNetAdapterReceiveScalingDisable](/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_disable)*
    3. *[EvtNetAdapterReceiveScalingSetHashSecretKey](/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_hash_secret_key)*
    4. *[EvtNetAdapterReceiveScalingSetIndirectionEntries](/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_indirection_entries)*
4. 根据需要设置 RSS 功能结构的 **SynchronizeSetIndirectionEntries** 。
5. 将初始化的 RSS 功能结构传递到 [NetAdapterSetReceiveScalingCapabilities](/windows-hardware/drivers/ddi/netreceivescaling/nf-netreceivescaling-netadaptersetreceivescalingcapabilities) 方法。

## <a name="enabling-and-disabling-rss"></a>启用和禁用 RSS

设置 RSS 功能后，系统将继续执行驱动程序的启动顺序。 创建数据路径队列的最后一个步骤完成后，NetAdapterCx 开始调用驱动程序的 RSS 回调。 此时，可以根据系统的需要启用和禁用 RSS。 

> [!IMPORTANT]
> 启用或禁用 RSS 时， **不** 应清除或重置间接寻址表。 框架将设置您的初始间接寻址表状态。

### <a name="enabling-rss"></a>启用 RSS

NetAdapterCx 通过调用驱动程序的 *[EvtNetAdapterReceiveScalingEnable](/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_enable)* 回调来启用 RSS。 在此回调的上下文中，通常会在硬件中启用控制位。 

有关启用 RSS 的代码示例，请参阅 *[EvtNetAdapterReceiveScalingEnable](/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_enable)*。

### <a name="disabling-rss"></a>禁用 RSS

NetAdapterCx 通过调用驱动程序的 *[EvtNetAdapterReceiveScalingDisable](/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_disable)* 回调来禁用 RSS。 此时，通常会在 *EvtNetAdapterReceiveScalingEnable*中禁用先前设置的硬件中的控制位。 

有关禁用 RSS 的代码示例，请参阅 *[EvtNetAdapterReceiveScalingDisable](/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_disable)*。

## <a name="setting-the-hash-secret-key"></a>设置哈希密钥

启用 RSS 后，NetAdapterCx 会调用 *[EvtNetAdapterReceiveScalingSetHashSecretKey](/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_hash_secret_key)* 回调为驱动程序提供 NIC 在验证哈希计算时应使用的哈希机密密钥。 如果哈希机密密钥发生更改，则可以随时调用此回调。 

有关设置哈希密钥的代码示例，请参阅 *[EvtNetAdapterReceiveScalingSetHashSecretKey](/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_hash_secret_key)*。

## <a name="moving-indirection-table-entries"></a>移动间接表项

当 RSS 在系统上运行时，上层协议驱动程序将监视处理器工作负荷并维护将接收队列映射到处理器的间接寻址表。 当协议驱动程序需要重新平衡 RSS 中的处理器工作负荷时，它首先为每个间接表项的新映射计算新的处理器。 然后，协议将此信息传递给 NetAdapterCx，这会代表 NIC 客户端驱动程序处理将接收队列和硬件中断向量映射到正确处理器的复杂性。 NetAdapterCx 将新的间接寻址表存储在 [NET_ADAPTER_RECEIVE_SCALING_INDIRECTION_ENTRIES](/windows-hardware/drivers/ddi/netreceivescaling/ns-netreceivescaling-_net_adapter_receive_scaling_indirection_entries) 结构中，并将其映射到接收队列 id，并将其传递给你的驱动程序（如果它调用 *[EvtNetAdapterReceiveScalingSetIndirectionEntries](/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_indirection_entries)* 回调函数）。 

在此回调中，将 NIC 的间接寻址表中的每个项移动到指定的接收队列。 **NET_ADAPTER_RECEIVE_SCALING_INDIRECTION_ENTRIES**数组中的每个[NET_ADAPTER_RECEIVE_SCALING_INDIRECTION_ENTRY](/windows-hardware/drivers/ddi/netreceivescaling/ns-netreceivescaling-_net_adapter_receive_scaling_indirection_entry)结构都包含表中该条目的哈希索引、要向其分配条目的新接收队列，以及指示单个移动是否成功的状态字段。 

为硬件接收队列分配索引条目的方法取决于 NIC 的设计以及其拥有的接收队列的数量。 有关详细信息和代码示例，请参阅 *[EvtNetAdapterReceiveScalingSetIndirectionEntries](/windows-hardware/drivers/ddi/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_indirection_entries)*。