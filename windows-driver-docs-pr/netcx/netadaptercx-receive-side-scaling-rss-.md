---
title: NetAdapterCx 接收方缩放 (RSS)
description: NetAdapterCx 接收方缩放 (RSS)
ms.assetid: 85A819E2-6352-4DE9-9689-3DCEB9B0AAD8
keywords:
- WDF 网络适配器类扩展接收方伸缩、 NetAdapterCx 接收方缩放，NetAdapterCx RSS NetAdapter RSS
ms.date: 07/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8afa43147869c8add2237cf6fa1a46e44644cdee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562431"
---
# <a name="netadaptercx-receive-side-scaling-rss"></a>NetAdapterCx 接收方缩放 (RSS)

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

接收的方缩放 (RSS) 是一种网络驱动程序技术实现高效的网络分布在多处理器系统中接收处理跨多个 Cpu。 RSS 可改进系统性能，并通过利用所有可用的处理器的强大功能在系统中并动态地重新平衡 CPU 的工作负荷提高网络可伸缩性。 

本主题是重点强调了 RSS NetAdapterCx 客户端驱动程序，并假定你了解 RSS 概念和术语。 有关 RSS 的详细信息一般情况下，包括关系图 RSS 在不同的硬件情况下，请参阅[接收方伸缩](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-receive-side-scaling2)。

## <a name="overview-of-rss-in-netadaptercx"></a>NetAdapterCx 中的 RSS 的概述

RSS NetAdapterCx 中的重点介绍易于配置，启用和停用的简单性和处理器中断复杂性的抽象。 支持 RSS 的 NIC 的客户端驱动程序只需满足以下三个条件，以支持 RSS 中 NetAdapterCx:

1. 该驱动程序必须设置 RSS 功能启动网络适配器，但在通过调用[ **NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart)。 这包括实现四个 RSS 回调和 RSS 功能结构中注册它们。
2. 驱动程序的数据路径队列必须创建并准备好接受请求。
3. 该驱动程序必须位于*D0*电源状态。

NetAdapterCx 中的 RSS 的设计可确保系统将不调用客户端的 RSS 回调并的恰好结束之前启用 RSS[强化序列](power-up-sequence-for-a-netadaptercx-client-driver.md)。 客户端无需管理间接表移动请求或处理所需要的一切准备就绪之前其他 RSS 事件。 

更高版本，当卸载该驱动程序，NetAdapterCx 将不会调用 RSS 回调后数据路径队列期间在销毁[电源关闭序列](power-down-sequence-for-a-netadaptercx-client-driver.md)。 由于数据路径队列依据的第一步在关闭期间，这意味着，客户端不需要在关闭期间在任何其他阶段处理可能 RSS 事件。

## <a name="setting-rss-capabilities"></a>设置 RSS 功能

若要开始使用 NetAdapterCx 中的 RSS，请执行以下步骤：

1. 当从网络适配器，有关您的硬件的 RSS 功能和限制使用告诉系统[NET_ADAPTER_RECEIVE_SCALING_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/ns-netreceivescaling-_net_adapter_receive_scaling_capabilities)结构。
2. 通过调用初始化功能结构[NET_ADAPTER_RECEIVE_SCALING_CAPABILITIES_INIT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nf-netreceivescaling-net_adapter_receive_scaling_capabilities_init)。 
3. 在初始化 RSS 功能结构，该结构的 RSS 回调将成员设置为注册您的这些回调的实现：
    1. *[EvtNetAdapterReceiveScalingEnable](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_enable)*
    2. *[EvtNetAdapterReceiveScalingDisable](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_disable)*
    3. *[EvtNetAdapterReceiveScalingSetHashSecretKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_hash_secret_key)*
    4. *[EvtNetAdapterReceiveScalingSetIndirectionEntries](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_indirection_entries)*
4. 设置的 RSS 功能结构**SynchronizeSetIndirectionEntries**根据需要。
5. 传递到已初始化的 RSS 功能结构[NetAdapterSetReceiveScalingCapabilities](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nf-netreceivescaling-netadaptersetreceivescalingcapabilities)方法。

## <a name="enabling-and-disabling-rss"></a>启用和禁用 RSS

设置 RSS 功能后，系统将继续您的驱动程序的启动顺序。 NetAdapterCx 开始创建数据路径队列的最后一步完成后调用您的驱动程序的 RSS 回调。 在此情况下，RSS 可以启用和禁用，因为所需的系统。 

> [!IMPORTANT]
> 您应该**不**清除或重置您的间接寻址表时启用或禁用 RSS。 该框架将设置你的初始间接表状态。

### <a name="enabling-rss"></a>启用 RSS

NetAdapterCx 通过调用您的驱动程序启用了 RSS *[EvtNetAdapterReceiveScalingEnable](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_enable)* 回调。 在此回调的上下文中，通常在您的硬件中启用控制位。 

有关启用 RSS 的代码示例，请参阅 *[EvtNetAdapterReceiveScalingEnable](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_enable)*。

### <a name="disabling-rss"></a>禁用 RSS

NetAdapterCx 通过调用您的驱动程序禁用 RSS *[EvtNetAdapterReceiveScalingDisable](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_disable)* 回调。 在这里，你通常控制位中禁用你之前设置中的硬件*EvtNetAdapterReceiveScalingEnable*。 

禁用 RSS 的代码示例，请参阅 *[EvtNetAdapterReceiveScalingDisable](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_disable)*。

## <a name="setting-the-hash-secret-key"></a>设置哈希密钥

一旦启用了 RSS，调用 NetAdapterCx *[EvtNetAdapterReceiveScalingSetHashSecretKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_hash_secret_key)* 回调 NIC 与哈希密钥提供您的驱动程序应使用验证哈希计算。 可以在任何时候如果哈希密钥更改 RSS 的运行时调用此回调。 

设置哈希机密密钥的代码示例，请参阅 *[EvtNetAdapterReceiveScalingSetHashSecretKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_hash_secret_key)*。

## <a name="moving-indirection-table-entries"></a>移动间接表条目

RSS 在系统上运行时，上层协议驱动程序将监视处理器工作负荷和维护映射的间接寻址表接收队列到处理器。 当需要重新平衡 RSS 在处理器工作负荷协议驱动程序时，它首先计算新处理器到每个间接表条目的新映射。 然后该协议将此信息传递到 NetAdapterCx，映射的复杂性接收的处理队列和到正确的处理器的硬件中断向量代表 NIC 客户端驱动程序。 NetAdapterCx 将新的间接寻址表，存储映射，以接收队列 Id 中的条目[NET_ADAPTER_RECEIVE_SCALING_INDIRECTION_ENTRIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/ns-netreceivescaling-_net_adapter_receive_scaling_indirection_entries)结构，并将其传递到您的驱动程序时它将调用*[EvtNetAdapterReceiveScalingSetIndirectionEntries](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_indirection_entries)* 回调函数。 

在此回调中，你将移动的每个条目 NIC 的间接寻址表中到指定的接收队列。 每个[NET_ADAPTER_RECEIVE_SCALING_INDIRECTION_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/ns-netreceivescaling-_net_adapter_receive_scaling_indirection_entry)结构**NET_ADAPTER_RECEIVE_SCALING_INDIRECTION_ENTRIES**数组包含在表中，该条目的哈希索引的新接收队列要向其分配项，而状态字段指示单个移动已成功与否。 

将索引项分配给硬件的方法接收队列在取决于您的 NIC 和它具有接收队列数目的设计。 有关详细信息和代码示例，请参阅 *[EvtNetAdapterReceiveScalingSetIndirectionEntries](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netreceivescaling/nc-netreceivescaling-evt_net_adapter_receive_scaling_set_indirection_entries)*。
