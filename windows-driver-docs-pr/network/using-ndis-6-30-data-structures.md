---
title: 使用 NDIS 6.30 数据结构
description: 使用 NDIS 6.30 数据结构
ms.assetid: 0CAD1CCE-5AF6-4EBD-85C9-040FA0D1C141
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0410a32d27aba08acc4770be800d51d1e7eccf9e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211573"
---
# <a name="using-ndis-630-data-structures"></a>使用 NDIS 6.30 数据结构


NDIS 可支持同一数据结构的多个版本。 对于 Windows 8 和 Windows Server 2012 操作系统，使用结构的 NDIS 6.30 版本的微型端口驱动程序必须使用正确的版本和大小值初始化结构的 **标头** 成员。 **标头**成员是一个[**ndis \_ 对象 \_ 标头**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)结构，驱动程序必须将**标头**成员的**修订版**成员和**size**成员值初始化为 ndis 6.30 版本和大小值。

**注意**   若要确定正确的版本和大小信息，请参阅每个包含**标头**成员的结构的参考页。 对于包含 **标头** 成员并且已针对 ndis 6.30 更新的结构，其引用页包含 ndis 6.30 驱动程序的新信息。 如果没有针对 NDIS 6.30 的结构的更新，则为早期版本的 NDIS 提供的信息也适用于 NDIS 6.30 驱动程序。

 

为 NDIS 6.30 更新了以下结构：

- [**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)
- [**NDIS \_ 微型端口 \_ 适配器 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_attributes)
- [**NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)
- [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 辅助 \_ 特性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)
- [**NDIS \_ 微型端口 \_ 适配器 \_ 本机 \_ 802 \_ 11 \_ 属性**](/previous-versions/windows/hardware/wireless/ff565926(v=vs.85))
- [**NDIS \_ 网络 \_ 缓冲区 \_ 列表 \_ 筛选 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)
- [**NDIS \_ NIC \_ 交换机 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)
- [**NDIS \_ 卸载**](/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_offload_handle)
- [**NDIS \_ 卸载 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)
- [**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)
- [**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)
- [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)
- [**NDIS \_ 接收 \_ 筛选器 \_ 信息 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)
- [**NDIS \_ 接收 \_ 筛选器 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)
- [**NDIS \_ 接收 \_ 队列 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info)
- [**NDIS \_ 接收 \_ 队列 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)
- [**NDIS \_ 接收 \_ 缩放 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)
- [**NDIS \_ RSS \_ 处理器 \_ 信息**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_processor_info)
- [**NDIS \_ SHARED \_ MEMORY \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_shared_memory_parameters)
 

