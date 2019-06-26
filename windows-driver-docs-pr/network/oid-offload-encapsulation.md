---
title: OID_OFFLOAD_ENCAPSULATION
description: 本主题介绍 OID_OFFLOAD_ENCAPSULATION 对象标识符 (OID)。
ms.assetid: 8B5BE43C-1004-427A-B16D-5A2AA34C96CD
keywords:
- OID_OFFLOAD_ENCAPSULATION，WDK Oid，WDK，WDK 网络 Oid 的网络对象标识符
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: e13eb8eab9cc4e2529d5ccf0771360ef24606f16
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383249"
---
# <a name="oidoffloadencapsulation"></a>OID_OFFLOAD_ENCAPSULATION

作为查询请求，基础驱动程序使用 OID_OFFLOAD_ENCAPSULATION OID 来获取当前任务的基础的微型端口适配器卸载封装设置。 NDIS 处理此 OID 查询的微型端口驱动程序。

Set 请求，作为基础驱动程序使用 OID_OFFLOAD_ENCAPSULATION OID 来设置任务的基础的微型端口适配器卸载封装设置。 支持任务卸载的微型端口驱动程序必须处理此 OID 集请求。

## <a name="remarks"></a>备注

InformationBuffer 隶属[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含[NDIS_OFFLOAD_ENCAPSULATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_offload_encapsulation)结构。

### <a name="miniport-drivers"></a>微型端口驱动程序

如果微型端口驱动程序不支持卸载和此 OID，则驱动程序应返回 NDIS_STATUS_NOT_SUPPORTED。

微型端口驱动程序必须使用的内容[NDIS_OFFLOAD_ENCAPSULATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_offload_encapsulation)结构，以更新当前报告的 TCP 卸载功能。 更新后，微型端口驱动程序必须报告的当前任务卸载能力[NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)状态指示。 此状态指示可确保所有基础协议驱动程序使用新的功能信息更新。

使用此 OID 激活所有已配置或启用卸载功能，或停用所有卸载 （换而言之，硬件开始执行卸载）。 它不提供对单个卸载进行精细控制。 相反， [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)用于配置单个卸载，还可以激活它们。 通常情况下，还可以配置和使用 OID_TCP_OFFLOAD_PARAMETERS 激活大多数 TCP/IP 任务卸载。

但是，此 OID NDIS_OFFLOAD_ENCAPSULATION 结构还介绍了两个不受 OID_TCP_OFFLOAD_PARAMETERS 的其他封装类型[NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)结构：**NDIS_ENCAPSULATION_IEEE_802_3**并**NDIS_ENCAPSULATION_IEEE_LLC_SNAP_ROUTED**。 微型端口驱动程序需要处理这种不同的 Oid 涵盖的封装类型的差异。

如果此 OID 由协议驱动程序，若要停用所有卸载颁发**已启用**NDIS_OFFLOAD_ENCAPSULATION 成员的成员将设置为 NDIS_OFFLOAD_SET_OFF。

### <a name="setting-encapsulation-protocol-drivers"></a>设置封装 （协议驱动程序）

确定系统封装要求后，协议驱动程序设置 OID_OFFLOAD_ENCAPSULATION。 协议驱动程序可以确定从基础的微型端口适配器的功能[NDIS_BIND_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)结构，要么查询[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)。 协议驱动程序必须支持至少一个卸载服务的微型端口适配器封装类型设置。

如果微型端口驱动程序支持任何支持请求的封装类型的卸载类型，则驱动程序必须返回 NDIS_STATUS_SUCCESS OID_OFFLOAD_ENCAPSULATION 一组响应。 否则，微型端口驱动程序应返回 NDIS_STATUS_INVALID_PARAMETER。

对于发送操作，协议驱动程序可以通过使用只有这些微型端口适配器支持使用所需的封装类型的卸载类型发出发送请求。 因此，如果 OID 设置 OID_OFFLOAD_ENCAPSULATION 失败的请求，协议驱动程序必须不会定向到该微型端口适配器的发送请求中使用卸载的任何设置。

对于接收操作、 微型端口驱动程序必须启动校验和或 Internet 协议安全性 (IPsec) OID 收到后设置 OID_OFFLOAD_ENCAPSULATION 请求之前卸载服务。

### <a name="obtaining-current-encapsulation-settings-protocol-drivers"></a>获取当前封装设置 （协议驱动程序）

协议驱动程序可以仅在设置 OID_OFFLOAD_ENCAPSULATION OID 后发出 OID_OFFLOAD_ENCAPSULATION 查询。

使用响应 NDIS [NDIS_OFFLOAD_ENCAPSULATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_offload_encapsulation)结构，其中包含当前封装设置。

协议驱动程序必须准备好处理任何 NDIS_STATUS_Xxx 失败代码。 如果发生故障，协议驱动程序必须不尝试执行任何定向到受影响的微型端口适配器的卸载操作。

### <a name="see-also"></a>请参阅

[NDIS_BIND_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)  
[NDIS_OFFLOAD_ENCAPSULATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_offload_encapsulation)  
[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)  
[NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)  
[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

