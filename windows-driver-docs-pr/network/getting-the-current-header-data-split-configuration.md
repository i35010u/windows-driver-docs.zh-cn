---
title: 获取当前的标头数据拆分配置
description: 获取当前的标头数据拆分配置
ms.assetid: 62c5e362-4e19-465d-85a8-a8277cb46f5d
keywords:
- 标头-数据拆分 WDK，配置
- 当前标头-数据拆分配置 WDK 网络
- 状态信息 WDK 标头-数据拆分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bcc91cbfae555f42b3c57186889fad58d8cf656
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842173"
---
# <a name="getting-the-current-header-data-split-configuration"></a>获取当前的标头数据拆分配置





为了获取微型端口适配器的当前标头-数据拆分设置，过量驱动程序或用户模式应用程序可以查询[OID\_GEN\_HD\_拆分\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-current-config)OID。 但是，过量驱动程序应使用 NDIS 在初始化和状态指示过程中提供的信息。

系统管理员可以使用与 OID 关联的 GUID\_GEN\_HD\_通过 WMI 接口拆分\_当前\_配置 OID。 有关标头数据拆分 WMI Guid 的详细信息，请参阅[对标头数据拆分的 WMI 支持](wmi-support-for-header-data-split.md)。

NDIS 处理[OID\_GEN\_HD\_代表微型端口驱动程序拆分\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-current-config)。 NDIS 根据微型端口驱动程序初始化属性和[**ndis\_状态\_HD\_拆分\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)状态指示，来维护当前的标头数据拆分配置信息。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含[**ndis\_HD\_SPLIT\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)结构。 NDIS 还提供 NDIS\_HD\_在初始化期间将当前\_CONFIG 结构\_拆分为过量驱动程序，并提供状态指示。

当微型端口驱动程序接收[OID\_GEN\_HD\_拆分\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters)设置的请求时，驱动程序必须使用 NDIS\_[**HD\_split\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)结构的内容来更新当前小型端口适配器的配置。 更新完成后，微型端口驱动程序必须将[**NDIS\_状态\_HD\_拆分\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)状态指示报告更改。 状态指示可确保所有的过量驱动程序都用新信息更新。

当 NDIS 调用 NDIS 6.1 或更高版本协议驱动程序的[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数时，ndis 会提供一个[**ndis\_将\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构与一个指向[**NDIS\_HD\_SPLIT\_当前 @no__ 的指针绑定t_11_ 配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)结构。

当 NDIS 调用 NDIS 6.1 或更高版本的筛选器驱动程序的[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)函数时，ndis 会提供一个[**NDIS\_筛选器\_将\_参数结构附加**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)到指向 NDIS\_HD\_SPLIT\_当前\_配置结构。

 

 





