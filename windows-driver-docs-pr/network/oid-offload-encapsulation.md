---
title: OID_OFFLOAD_ENCAPSULATION
description: 本主题介绍) OID_OFFLOAD_ENCAPSULATION 对象标识符 (OID。
keywords:
- OID_OFFLOAD_ENCAPSULATION，WDK Oid，WDK 网络对象标识符，WDK 网络 Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 380d20d289bbba0cfd0fc6e6aa8d82bb93202ffa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837105"
---
# <a name="oid_offload_encapsulation"></a>OID_OFFLOAD_ENCAPSULATION

作为查询请求，过量驱动程序使用 OID_OFFLOAD_ENCAPSULATION OID 获取基础微型端口适配器的当前任务卸载封装设置。 NDIS 处理微型端口驱动程序的此 OID 查询。

作为一个集请求，过量驱动程序使用 OID_OFFLOAD_ENCAPSULATION OID 来设置基础微型端口适配器的任务卸载封装设置。 支持任务卸载的微型端口驱动程序必须处理此 OID 设置请求。

## <a name="remarks"></a>备注

[NDIS_OID_REQUEST](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 InformationBuffer 成员包含[NDIS_OFFLOAD_ENCAPSULATION](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation)结构。

### <a name="miniport-drivers"></a>微型端口驱动程序

如果微型端口驱动程序不支持卸载和此 OID，则驱动程序应返回 NDIS_STATUS_NOT_SUPPORTED。

微型端口驱动程序必须使用 [NDIS_OFFLOAD_ENCAPSULATION](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation) 结构的内容来更新当前报告的 TCP 卸载功能。 更新后，微型端口驱动程序必须报告当前的任务卸载功能，并 [NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md) 状态指示。 此状态指示可确保所有的过量协议驱动程序都用新功能信息进行更新。

此 OID 用于激活所有已配置或已启用的卸载，或停用所有卸载 (换言之，硬件开始执行卸载) 。 它不提供对各个卸载的精细控制。 相反， [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) 用于配置单个卸载，还可以激活。 通常，可以通过 OID_TCP_OFFLOAD_PARAMETERS 来配置和激活大多数 TCP/IP 任务卸载。

但是，此 OID 的 NDIS_OFFLOAD_ENCAPSULATION 结构还介绍了 OID_TCP_OFFLOAD_PARAMETERS 的 [NDIS_OFFLOAD_PARAMETERS](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters) 结构未涵盖的其他两种封装类型： **NDIS_ENCAPSULATION_IEEE_802_3** 和 **NDIS_ENCAPSULATION_IEEE_LLC_SNAP_ROUTED**。 微型端口驱动程序需要处理不同 Oid 所涵盖的封装类型中的这一差异。

如果此 OID 由协议驱动程序颁发以停用所有卸载，则 NDIS_OFFLOAD_ENCAPSULATION 成员的 **已启用** 成员将设置为 NDIS_OFFLOAD_SET_OFF。

### <a name="setting-encapsulation-protocol-drivers"></a> (协议驱动程序设置封装) 

确定系统封装要求后 OID_OFFLOAD_ENCAPSULATION 设置协议驱动程序。 协议驱动程序可以从 [NDIS_BIND_PARAMETERS](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters) 结构或通过查询 [OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)来确定基础微型端口适配器的功能。 协议驱动程序必须在至少一个卸载服务上设置一个小型端口适配器支持的封装类型。

如果微型端口驱动程序支持支持请求的封装类型的任何卸载类型，则驱动程序必须返回 NDIS_STATUS_SUCCESS 以响应一组 OID_OFFLOAD_ENCAPSULATION。 否则，微型端口驱动程序应返回 NDIS_STATUS_INVALID_PARAMETER。

对于发送操作，协议驱动程序只能使用微型端口适配器支持的卸载类型和所需的封装类型发出发送请求。 因此，如果 OID OID_OFFLOAD_ENCAPSULATION 的请求失败，则协议驱动程序不得使用发送请求中定向到该微型端口适配器的任何卸载设置。

对于接收操作，微型端口驱动程序不得开始 (IPsec) 卸载服务的校验和或 Internet 协议安全，直到收到 OID_OFFLOAD_ENCAPSULATION 的 OID 设置请求。

### <a name="obtaining-current-encapsulation-settings-protocol-drivers"></a> (协议驱动程序获取当前封装设置) 

协议驱动程序只能在设置 OID_OFFLOAD_ENCAPSULATION OID 后发出 OID_OFFLOAD_ENCAPSULATION 查询。

NDIS 使用包含当前封装设置的 [NDIS_OFFLOAD_ENCAPSULATION](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation) 结构进行响应。

协议驱动程序必须准备好处理任何 NDIS_STATUS_Xxx 故障代码。 如果发生故障，协议驱动程序不得尝试执行任何卸载操作，这些操作将定向到受影响的微型端口适配器。

### <a name="see-also"></a>请参阅

[NDIS_BIND_PARAMETERS](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)  
[NDIS_OFFLOAD_ENCAPSULATION](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation)  
[NDIS_OID_REQUEST](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)  
[NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)  
[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 
