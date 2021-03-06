---
title: OID_QOS_OFFLOAD_HARDWARE_CAPABILITIES
description: OID_QOS_OFFLOAD_HARDWARE_CAPABILITIES 获取用于获取微型端口适配器的 vmQoS 卸载硬件功能的过量驱动程序问题。
ms.assetid: ''
ms.date: 10/30/2020
keywords: -从 Windows Vista 开始 OID_QOS_OFFLOAD_HARDWARE_CAPABILITIES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8631dca8b33f8538d7fb0922e80e78f33250abe4
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250520"
---
# <a name="oid_qos_offload_hardware_capabilities"></a>OID_QOS_OFFLOAD_HARDWARE_CAPABILITIES


过量驱动程序发出 OID_QOS_OFFLOAD_HARDWARE_CAPABILITIES 的 OID 查询请求，以获取服务质量 (QoS) 卸载微型端口适配器的硬件功能。

成功从 OID 查询请求返回后， [**NDIS_OID_REQUEST**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS_QOS_OFFLOAD_CAPABILITIES**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_offload_capabilities)结构的指针。

## <a name="remarks"></a>备注

[**NDIS_QOS_OFFLOAD_CAPABILITIES**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_offload_capabilities)结构指定了硬件和当前硬件服务质量 (QOS) 的卸载功能。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理适用于微型端口驱动程序的 OID_QOS_OFFLOAD_HARDWARE_CAPABILITIES 的 OID 查询请求，并返回以下状态代码之一。

|状态代码|说明|
|--- |--- |
|NDIS_STATUS_SUCCESS|OID 请求已成功完成。|
|NDIS_STATUS_NOT_SUPPORTED|微型端口驱动程序不支持 NDIS QoS 接口。|
|NDIS_STATUS_BUFFER_TOO_SHORT|信息缓冲区的长度不足以获得返回的数据。|
|NDIS_STATUS_Xxx|由于其他原因，请求失败。|

 

## <a name="requirements"></a>要求

|要求|值|
|--- |--- |
|Version|在 NDIS 6.85 和更高版本中受支持。|
|标题|Ntddndis (包含 Ndis .h) |

## <a name="see-also"></a>请参阅

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS_QOS_OFFLOAD_CAPABILITIES**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_offload_capabilities)

[OID_QOS_OFFLOAD_CURRENT_CAPABILITIES](oid-qos-offload-current-capabilities.md)

 
