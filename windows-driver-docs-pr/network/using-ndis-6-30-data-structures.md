---
title: 使用 NDIS 6.30 数据结构
description: 使用 NDIS 6.30 数据结构
ms.assetid: 0CAD1CCE-5AF6-4EBD-85C9-040FA0D1C141
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a27846a7057cccc2510b9428cefae14c463b07d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842984"
---
# <a name="using-ndis-630-data-structures"></a>使用 NDIS 6.30 数据结构


NDIS 可支持同一数据结构的多个版本。 对于 Windows 8 和 Windows Server 2012 操作系统，使用结构的 NDIS 6.30 版本的微型端口驱动程序必须使用正确的版本和大小值初始化结构的**标头**成员。 **标头**成员是一个[**NDIS\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)结构，驱动程序必须将该**标头**成员的**修订版**成员和**size**成员值初始化为 ndis 6.30 版本和大小值。

**请注意**  确定正确的版本和大小信息，请参阅每个包含**标头**成员的结构的参考页。 对于包含**标头**成员并且已针对 ndis 6.30 更新的结构，其引用页包含 ndis 6.30 驱动程序的新信息。 如果没有针对 NDIS 6.30 的结构的更新，则为早期版本的 NDIS 提供的信息也适用于 NDIS 6.30 驱动程序。

 

为 NDIS 6.30 更新了以下结构：

- [ **\_绑定\_参数的 NDIS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)
- [ **\_适配器\_属性的 NDIS\_微型端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_attributes)
- [**NDIS\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)
- [**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)
- [**NDIS\_微型端口\_适配器\_本机\_802\_11\_属性**](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff565926(v=vs.85))
- [**NDIS\_NET\_缓冲器\_列表\_筛选\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_filtering_info)
- [**NDIS\_NIC\_交换机\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)
- [**NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_offload_handle)
- [**NDIS\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)
- [**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)
- [**NDIS\_PM\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)
- [**NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)
- [**NDIS\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)
- [**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)
- [**NDIS\_接收\_队列\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_info)
- [**NDIS\_接收\_队列\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)
- [**NDIS\_接收\_缩放\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)
- [ **\_处理器的 NDIS\_\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_processor_info)
- [**NDIS\_共享\_内存\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_shared_memory_parameters)
 

 





