---
title: OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES
description: 本主题介绍) OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES 对象标识符 (OID。
ms.assetid: E90EC9E5-4667-4CBF-8812-06FB45331368
keywords:
- OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES，WDK Oid，WDK 网络对象标识符，WDK 网络 Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc34c077ccf1e4432b4df62cffc314802409d497
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213801"
---
# <a name="oid_tcp_connection_offload_hardware_capabilities"></a>OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES

作为查询请求，OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES OID 将报告底层微型端口适配器的当前连接卸载硬件功能。 用户模式应用程序 (或可能过量的驱动程序) 可以查询此 OID，以确定基础微型端口适配器的连接卸载硬件功能。 系统管理员可以使用此 OID 通过 Microsoft Windows Management Instrumentation (WMI) 接口。

不支持设置请求。

## <a name="remarks"></a>备注

NDIS 处理微型端口驱动程序的此 OID。 微型端口驱动程序报告微型端口适配器连接将硬件功能卸载到 NDIS。 有关将连接卸载硬件功能从微型端口驱动程序和 NDIS 传递到过量驱动程序的信息，请参阅 [NDIS_TCP_CONNECTION_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)。

[NDIS_OID_REQUEST](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含[NDIS_TCP_CONNECTION_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)结构。

为响应 OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES，NDIS_TCP_CONNECTION_OFFLOAD 的 **封装** 成员定义微型端口适配器的当前数据包封装硬件功能。 NDIS 提供 **封装** 成员中提供的标志的按位 "或"。 NDIS_TCP_CONNECTION_OFFLOAD 的其他成员包含各种连接卸载服务的设置。 有关封装和其他功能的详细信息，请参阅 [NDIS_TCP_CONNECTION_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload) 和 [NDIS_OFFLOAD_PARAMETERS](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)。


### <a name="see-also"></a>另请参阅

[NDIS_OFFLOAD_PARAMETERS](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)  
[NDIS_OID_REQUEST](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)  
[NDIS_TCP_CONNECTION_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 