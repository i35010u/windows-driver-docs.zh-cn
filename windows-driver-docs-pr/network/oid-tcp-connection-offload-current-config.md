---
title: OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG
description: 本主题介绍 OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG 对象标识符（OID）。
ms.assetid: 29CB74B1-8D7F-4EC2-AAAC-93D454824031
keywords:
- OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG，WDK Oid，WDK 网络对象标识符，WDK 网络 Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff0f7d25253f376a8fbd58ca83d1ffc24e8afddf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843912"
---
# <a name="oid_tcp_connection_offload_current_config"></a>OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG

作为查询请求，管理应用程序（或可能过量的驱动程序）可以使用 OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG OID 来确定基础微型端口适配器的当前启用的连接卸载功能。 系统管理员可以通过 Microsoft Windows Management Instrumentation （WMI）接口使用此 OID。

不支持设置请求。

## <a name="remarks"></a>备注

NDIS 处理微型端口驱动程序的此 OID。 微型端口驱动程序报告微型端口适配器连接卸载设置到 NDIS。 有关从微型端口驱动程序将连接卸载配置设置传递到 NDIS，以及从 NDIS 传递到过量驱动程序的信息，请参阅[NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)。

[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含[NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)结构。

为响应 OID_TCP_CONNECTION_OFFLOAD_CURRENT_CONFIG，NDIS_TCP_CONNECTION_OFFLOAD 的**封装**成员定义微型端口适配器的当前数据包封装配置。 NDIS 提供**封装**成员中提供的标志的按位 "或"。 NDIS_TCP_CONNECTION_OFFLOAD 的其他成员包含各种连接卸载服务的设置。 有关封装和其他功能的详细信息，请参阅[NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)和[NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)。


### <a name="see-also"></a>另请参阅

[NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)  
[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)  
[NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows Vista 及更高版本 |
| 标头 | Ntddndis （包括 Ndis .h） |

