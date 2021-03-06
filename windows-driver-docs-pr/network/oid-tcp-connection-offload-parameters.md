---
title: OID_TCP_CONNECTION_OFFLOAD_PARAMETERS
description: 本主题介绍) OID_TCP_CONNECTION_OFFLOAD_PARAMETERS 对象标识符 (OID。
keywords:
- OID_TCP_CONNECTION_OFFLOAD_PARAMETERS，WDK Oid，WDK 网络对象标识符，WDK 网络 Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbb6e71ec386f20d36518c372c0a91822736677c
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249163"
---
# <a name="oid_tcp_connection_offload_parameters"></a>OID_TCP_CONNECTION_OFFLOAD_PARAMETERS

作为查询请求，过量驱动程序可以使用 OID_TCP_CONNECTION_OFFLOAD_PARAMETERS OID 来确定基础微型端口适配器的当前连接卸载设置。 NDIS 处理微型端口驱动程序的此 OID 查询。

作为一个集请求，NDIS 和过量驱动程序使用 OID_TCP_CONNECTION_OFFLOAD_PARAMETERS OID 来设置基础微型端口适配器的连接卸载配置参数。 支持连接卸载的微型端口驱动程序必须处理此 OID 设置请求。 否则，OID_TCP_CONNECTION_OFFLOAD_PARAMETERS OID 对于微型端口驱动程序是可选的。

## <a name="remarks"></a>备注

[NDIS_OID_REQUEST](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含 [NDIS_TCP_CONNECTION_OFFLOAD_PARAMETERS](/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_tcp_connection_offload_parameters)结构。

> [!NOTE]
> 不要将 OID_TCP_CONNECTION_OFFLOAD_PARAMETERS 与管理应用程序用于启用或禁用 TCP 卸载功能的 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) OID 混淆。

### <a name="see-also"></a>请参阅

[NDIS_OID_REQUEST](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)  
[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 
