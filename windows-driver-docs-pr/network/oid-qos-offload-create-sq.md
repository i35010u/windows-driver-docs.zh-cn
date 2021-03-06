---
title: OID_QOS_OFFLOAD_CREATE_SQ
description: OID_QOS_OFFLOAD_CREATE_SQ 在微型端口适配器上创建新的计划程序队列 (SQ) 的驱动程序问题
ms.assetid: ''
ms.date: 10/30/2020
keywords: -从 Windows Vista 开始 OID_QOS_OFFLOAD_CREATE_SQ 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3077fd6ae41d7edae406538472749acc3f3dfa5a
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250440"
---
# <a name="oid_qos_offload_create_sq"></a>OID_QOS_OFFLOAD_CREATE_SQ

过量驱动程序发出 OID 设置 OID_QOS_OFFLOAD_CREATE_SQ 的请求，以在微型端口适配器上 (SQ) 创建新的计划程序队列。 调用方将 [**NDIS_OID_REQUEST**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员设置为包含指向 [**NDIS_QOS_SQ_PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-ndis_qos_sq_parameters)结构的指针。 **NDIS_QOS_SQ_PARAMETERS** 包含新 SQ 的参数。

## <a name="remarks"></a>备注

**NDIS_QOS_SQ_ID** 是一种 ULONG 值，NDIS 为 SQ 分配并分配。 此标识符对于每个微型端口适配器是唯一的。 值 **NDIS_QOS_DEFAULT_SQ_ID** 不是有效的 SQ ID，表示不使用 sq。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理微型端口驱动程序的 OID_QOS_OFFLOAD_CREATE_SQ OID 集请求，并返回以下状态代码之一。

|状态代码|说明|
|--- |--- |
|NDIS_STATUS_SUCCESS|OID 请求已成功完成。|
|NDIS_STATUS_INVALID_PARAMETER|**InformationBuffer** 的长度小于 NDIS_SIZEOF_QOS_SQ_PARAMETERS_REVISION_1 或 **InformationBuffer** **NDIS_QOS_DEFAULT_SQ_ID** 中 [**NDIS_QOS_SQ_PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-ndis_qos_sq_parameters)的 **SqId** 字段。 |
|NDIS_STATUS_Xxx|由于其他原因，请求失败。|

 

## <a name="requirements"></a>要求

|要求|值|
|--- |--- |
|Version|在 NDIS 6.85 和更高版本中受支持。|
|标题|Ntddndis (包含 Ndis .h) |

## <a name="see-also"></a>请参阅

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS_QOS_SQ_PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-ndis_qos_sq_parameters)

[**NDIS_QOS_OFFLOAD_CAPABILITIES**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_offload_capabilities)

[OID_QOS_HARDWARE_CAPABILITIES](oid-qos-hardware-capabilities.md)

[OID_QOS_OFFLOAD_UPDATE_SQ](oid-qos-offload-update-sq.md)

 
