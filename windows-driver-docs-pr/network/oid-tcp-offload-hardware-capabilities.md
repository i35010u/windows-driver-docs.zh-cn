---
title: OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES
description: 本主题介绍) OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES 对象标识符 (OID。
ms.assetid: 9958F93C-0D68-428B-A25C-7FF6E4F37702
keywords:
- OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES，WDK Oid，WDK 网络对象标识符，WDK 网络 Oid
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9c0130fc341b974a84cdd5650b40f2ea128890f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215216"
---
# <a name="oid_tcp_offload_hardware_capabilities"></a>OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES

作为查询请求，OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES OID 会报告微型端口适配器硬件的任务卸载硬件功能。 用户模式应用程序 (或可能过量的驱动程序) 可以查询此 OID，以确定基础微型端口适配器的任务卸载硬件功能。 系统管理员可以通过 Windows Management Instrumentation (WMI) 接口使用此 OID。

不支持设置请求。

## <a name="remarks"></a>备注

NDIS 处理微型端口驱动程序的此 OID。 微型端口驱动程序向 NDIS 报告微型端口适配器硬件功能。 有关将任务卸载硬件功能从微型端口驱动程序和 NDIS 驱动程序报告给过量驱动程序的信息，请参阅 [NDIS_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)。

[NDIS_OID_REQUEST](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含[NDIS_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构。 如果缓冲区不够大，NDIS 将返回 NDIS_STATUS_BUFFER_TOO_SHORT。

确定微型端口适配器的硬件功能后，上层应用程序或驱动程序可以使用 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) oid 来启用 [OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md) OID 当前报告为未启用的功能。

### <a name="see-also"></a>另请参阅

[NDIS_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)  
[NDIS_OID_REQUEST](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)  
[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)  
[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)  

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 