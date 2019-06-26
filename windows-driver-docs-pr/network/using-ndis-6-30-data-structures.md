---
title: 使用 NDIS 6.30 数据结构
description: 使用 NDIS 6.30 数据结构
ms.assetid: 0CAD1CCE-5AF6-4EBD-85C9-040FA0D1C141
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be2edb9c85534851bca190c3a3ef935b780261c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371800"
---
# <a name="using-ndis-630-data-structures"></a>使用 NDIS 6.30 数据结构


NDIS 可以支持多个版本的相同的数据结构。 对于 Windows 8 和 Windows Server 2012 操作系统，请使用 NDIS 6.30 版本的一种结构的微型端口驱动程序必须初始化**标头**具有正确的版本和大小的值结构的成员。 **标头**成员是[ **NDIS\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header)结构和驱动程序必须初始化**修订**成员和**大小**的成员值**标头**成员添加到 NDIS 6.30 版本和大小的值。

**请注意**  来确定正确的版本和大小信息，请参阅每个结构，其中包含的参考页**标头**成员。 结构中包含的参考页**标头**成员并且已更新 NDIS 6.30 包括 NDIS 6.30 驱动程序的新信息。 如果不会更新到结构的 NDIS 6.30，早期 NDIS 版本提供的信息也适用于 NDIS 6.30 驱动程序。

 

有关 NDIS 6.30 更新了以下结构：

- [**NDIS\_BIND\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)
- [**NDIS\_微型端口\_适配器\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_attributes)
- [**NDIS\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)
- [**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)
- [**NDIS\_微型端口\_适配器\_本机\_802\_11\_属性**](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff565926(v=vs.85))
- [**NDIS\_NET\_BUFFER\_LIST\_FILTERING\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)
- [**NDIS\_NIC\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)
- [**NDIS\_OFFLOAD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndischimney/ns-ndischimney-_ndis_offload_handle)
- [**NDIS\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)
- [**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)
- [**NDIS\_PM\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_parameters)
- [**NDIS\_RECEIVE\_FILTER\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)
- [**NDIS\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)
- [**NDIS\_RECEIVE\_FILTER\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)
- [**NDIS\_接收\_队列\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_info)
- [**NDIS\_RECEIVE\_QUEUE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)
- [**NDIS\_接收\_规模\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)
- [**NDIS\_RSS\_处理器\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_rss_processor_info)
- [**NDIS\_共享\_内存\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_shared_memory_parameters)
 

 





