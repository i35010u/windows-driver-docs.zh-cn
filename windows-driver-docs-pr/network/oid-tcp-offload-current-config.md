---
title: OID_TCP_OFFLOAD_CURRENT_CONFIG
description: 本主题介绍) OID_TCP_OFFLOAD_CURRENT_CONFIG 对象标识符 (OID。
keywords:
- OID_TCP_OFFLOAD_CURRENT_CONFIG，WDK Oid，WDK 网络对象标识符，WDK 网络 Oid
ms.date: 02/27/2020
ms.localizationpriority: medium
ms.openlocfilehash: 9093680617f0bfc7cac6054fd1f4b1fc6952299e
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249159"
---
# <a name="oid_tcp_offload_current_config"></a>OID_TCP_OFFLOAD_CURRENT_CONFIG

作为查询请求，管理应用程序 (或可能过量的驱动程序) 使用 OID_TCP_OFFLOAD_CURRENT_CONFIG OID 确定基础微型端口适配器的当前任务卸载配置设置。 系统管理员可以使用此 OID 通过 Microsoft Windows Management Instrumentation (WMI) 接口。

不支持设置请求。

## <a name="remarks"></a>备注

NDIS 处理微型端口驱动程序的此 OID。 微型端口驱动程序报告微型端口适配器卸载功能到 NDIS。 有关从微型端口驱动程序将任务卸载配置设置传递到 NDIS 以及从 NDIS 传递到过量驱动程序的信息，请参阅 NDIS_OFFLOAD。

[NDIS_OID_REQUEST](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含 [NDIS_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构。 **NDIS_OFFLOAD** 结构包含以下微型端口适配器功能：

- 标头信息，其中包含任务卸载版本。
- [NDIS_TCP_IP_CHECKSUM_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)结构中的校验和卸载信息。
- 大型发送卸载版本1在 [NDIS_TCP_LARGE_SEND_OFFLOAD_V1](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v1) 结构中 (LSOV1) 信息。
- Internet 协议安全在 [NDIS_IPSEC_OFFLOAD_V1](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1) 结构中 (IPsec) 信息。
- 大型发送卸载版本2在 [NDIS_TCP_LARGE_SEND_OFFLOAD_V2](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2) 结构中 (LSOV2) 信息。

为响应 OID_TCP_OFFLOAD_CURRENT_CONFIG，上列表中结构的 **封装** 成员定义了微型端口适配器的数据包封装功能。 NDIS 提供这些结构的 **封装** 成员中提供的标志的按位 "或"。 其他结构成员包含各种卸载服务的设置。 有关封装和其他功能的详细信息，请参阅 [NDIS_TCP_IP_CHECKSUM_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)、 [NDIS_TCP_LARGE_SEND_OFFLOAD_V1](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v1)、 [NDIS_IPSEC_OFFLOAD_V1](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)和 [NDIS_TCP_LARGE_SEND_OFFLOAD_V2](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)。

小型端口适配器必须支持其支持的所有类型的任务卸载的以太网封装。 其他类型的封装是可选的。

小型端口驱动程序应在初始化期间自动启用所有任务卸载功能。

### <a name="see-also"></a>请参阅

[NDIS_IPSEC_OFFLOAD_V1](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)  
[NDIS_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)  
[NDIS_OID_REQUEST](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)  
[NDIS_TCP_IP_CHECKSUM_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)  
[NDIS_TCP_LARGE_SEND_OFFLOAD_V2](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2) 
[NDIS_IPSEC_OFFLOAD_V1](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)  

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 
