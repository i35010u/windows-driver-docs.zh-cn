---
title: OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES
description: 本主题介绍 OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES 对象标识符 (OID)。
ms.assetid: E90EC9E5-4667-4CBF-8812-06FB45331368
keywords:
- OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES，WDK Oid，WDK，WDK 网络 Oid 的网络对象标识符
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e6217086d27f44d596aafa751444a7d98d03acb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386974"
---
# <a name="oidtcpconnectionoffloadhardwarecapabilities"></a>OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES

作为查询请求，OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES OID 报告基础的微型端口适配器的当前连接卸载硬件功能。 用户模式应用程序 （或可能是基础驱动程序） 可以查询此 OID 来确定连接卸载硬件功能的基础的微型端口适配器。 通过 Microsoft Windows Management Instrumentation (WMI) 界面，系统管理员可以使用此 OID。

不支持组的请求。

## <a name="remarks"></a>备注

NDIS 处理此 OID 的微型端口驱动程序。 微型端口驱动程序报告到 NDIS 的微型端口适配器连接卸载硬件功能。 有关将传递连接卸载硬件功能到 NDIS 从微型端口驱动程序和 NDIS 给基础驱动程序的信息，请参阅[NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)。

**InformationBuffer**的成员[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含[NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)结构。

OID_TCP_CONNECTION_OFFLOAD_HARDWARE_CAPABILITIES，响应**封装**NDIS_TCP_CONNECTION_OFFLOAD 成员定义的微型端口适配器当前数据包封装硬件功能。 NDIS 提供中提供的标志的按位 OR**封装**成员。 NDIS_TCP_CONNECTION_OFFLOAD 的其他成员包含各种连接卸载服务的设置。 有关封装和其他功能的详细信息，请参阅[NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)并[NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)。


### <a name="see-also"></a>请参阅

[NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)  
[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)  
[NDIS_TCP_CONNECTION_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

