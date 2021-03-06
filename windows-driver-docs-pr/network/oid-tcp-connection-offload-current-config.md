---
title: OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG
description: 本主题介绍) OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG 对象标识符 (OID。
keywords:
- OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG，WDK Oid，WDK 网络对象标识符，WDK 网络 Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: f602cb1bd6cb2ae74c90c8a30bf9794a398df689
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249166"
---
# <a name="oid_tcp_connection_offload_current_config"></a>OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG

作为查询请求，管理应用程序 (或可能过量的驱动程序) 可以使用 OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG OID 来确定基础微型端口适配器的当前启用的连接卸载功能。 系统管理员可以使用此 OID 通过 Microsoft Windows Management Instrumentation (WMI) 接口。

不支持设置请求。

## <a name="remarks"></a>备注

NDIS 处理微型端口驱动程序的此 OID。 微型端口驱动程序报告微型端口适配器连接卸载设置到 NDIS。 有关从微型端口驱动程序将连接卸载配置设置传递到 NDIS，以及从 NDIS 传递到过量驱动程序的信息，请参阅 [NDIS_TCP_CONNECTION_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)。

[NDIS_OID_REQUEST](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含 [NDIS_TCP_CONNECTION_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)结构。

为响应 OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG，NDIS_TCP_CONNECTION_OFFLOAD 的 **封装** 成员定义微型端口适配器的当前数据包封装配置。 NDIS 提供 **封装** 成员中提供的标志的按位 "或"。 NDIS_TCP_CONNECTION_OFFLOAD 的其他成员包含各种连接卸载服务的设置。 有关封装和其他功能的详细信息，请参阅 [NDIS_TCP_CONNECTION_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload) 和 [NDIS_OFFLOAD_PARAMETERS](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)。


### <a name="see-also"></a>请参阅

[NDIS_OFFLOAD_PARAMETERS](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)  
[NDIS_OID_REQUEST](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)  
[NDIS_TCP_CONNECTION_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 
