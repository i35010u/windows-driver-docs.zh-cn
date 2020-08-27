---
title: Hyper-v 可扩展交换机混合转发
description: 本部分介绍如何使用 Hyper-v 可扩展交换机进行混合转发
ms.assetid: 135CA734-1C92-4EEA-81DC-96A6A68ABBE8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cad55b4927c7a312f4215e2588a1620513162a8
ms.sourcegitcommit: 67efcd26f7be8f50c92b141ccd14c9c68f4412d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88902466"
---
# <a name="hybrid-forwarding"></a>混合转发

从 NDIS 6.40 (Windows Server 2012 R2 开始，Hyper-v 可扩展交换机体系结构支持通过可扩展交换机的 Hyper-v 网络虚拟化 (HNV) 组件和转发扩展来混合转发。

>[!NOTE]
>本页假设你熟悉 [使用通用路由封装的网络虚拟化 (NVGRE) 任务卸载](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md) 和 [Hyper-v 可扩展交换机概述](overview-of-the-hyper-v-extensible-switch.md)。

## <a name="nvgre-and-non-nvgre-packets"></a>NVGRE 和非 NVGRE 数据包

在混合转发环境中，有两种类型的数据包用于输入和保留 Hyper-v 可扩展交换机： NVGRE 数据包和非 NVGRE 数据包：

- NVGRE 数据包具有在 [NVGRE：使用通用路由封装的网络虚拟化](https://tools.ietf.org/html/rfc7637) Internet 草稿中指定的封装格式。 NVGRE 数据包由 Hyper-v 可扩展交换机的 HNV 组件转发。
- 非 NVGRE 数据包只是普通的网络数据包。 非 NVGRE 数据包由转发扩展转发 (或者，在没有转发扩展的情况下，可扩展交换机本身) 。

## <a name="flow-of-nvgre-and-non-nvgre-packets-through-the-switch"></a>通过交换机的 NVGRE 和非 NVGRE 数据包流

在入口数据路径中，在捕获和筛选扩展之后但在转发扩展之前，如果数据包为 NVGRE 数据包，则可扩展交换机会在[**NDIS \_ 交换机 \_ 转发 \_ 详细信息 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构中为数据包设置**NativeForwardingRequired**标志。 此结构包含在数据包的[**网络 \_ 缓冲区 \_ 列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的**NetBufferListInfo**成员中。

>[!NOTE]
>[**NET \_ BUFFER \_ 列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的**NetBufferListInfo**成员通常称为数据包的 "带外 (OOB) 数据"。

如果在数据包的 OOB 数据中设置了 **NativeForwardingRequired** 标志，则数据包为 NVGRE 数据包。 如果未设置，则数据包为非 NVGRE 数据包。

扩展应使用 [**网络 \_ 缓冲区 \_ 列表 \_ 切换 \_ 转发 \_ 详细信息**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail) 宏来检查 **NativeForwardingRequired** 标志的值。

NVGRE 和非 NVGRE 数据包的处理方式如下：

- Hyper-v 可扩展交换机的 HNV 组件转发 (即，确定) 所有 NVGRE 数据包的目标表
- HNV 组件根据需要执行 NVGRE 封装和和解。
- 转发扩展插件转发所有非 NVGRE 数据包。
- 转发扩展无法转发 NVGRE 数据包，但它可以执行与筛选扩展相同的筛选操作，包括添加或排除目标端口，甚至丢弃数据包。
- 如果没有转发扩展，Hyper-v 可扩展交换机会转发所有数据包。

有关详细信息，请参阅 [通过可扩展交换机数据路径的数据包流](packet-flow-through-the-extensible-switch-data-path.md)。

## <a name="support-for-third-party-network-virtualization"></a>支持第三方网络虚拟化

可以在 VM 网络适配器端口上将 **VirtualSubnetId** 配置为外部虚拟子网。 此功能已添加到启用转发扩展以提供第三方网络虚拟化解决方案。 在入口中，Hyper-v 可扩展交换机不会在这些数据包的[**网络 \_ 缓冲区 \_ 列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中设置**NativeForwardingRequired**标志。 转发扩展之后，可以根据需要修改数据包标头。 必须克隆正在修改的数据包，并将其 **ParentNetBufferList** 指针设置为原始 **网络 \_ 缓冲区 \_ 列表**。  (参阅 [克隆数据包流量](cloning-or-duplicating-packet-traffic.md)。 ) 

## <a name="related-topics"></a>相关主题

[将可扩展交换机目标端口数据添加到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)

[克隆数据包流量](cloning-or-duplicating-packet-traffic.md)

[转发扩展](forwarding-extensions.md)

[通过可扩展交换机数据路径传输的数据包流](packet-flow-through-the-extensible-switch-data-path.md)

[**网络 \_ 缓冲区 \_ 列表 \_ 交换机 \_ 转发 \_ 详细信息**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)

[**NDIS \_ 交换机 \_ 转发 \_ 详细信息 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)
