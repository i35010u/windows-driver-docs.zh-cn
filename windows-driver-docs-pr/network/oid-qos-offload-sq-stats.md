---
title: OID_QOS_OFFLOAD_SQ_STATS
description: 驱动程序问题 OID_QOS_OFFLOAD_SQ_STATS 获取当前在微型端口适配器上 (SQs) 的所有计划程序队列的列表。
ms.assetid: ''
ms.date: 10/30/2020
keywords: -从 Windows Vista 开始 OID_QOS_OFFLOAD_SQ_STATS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6a8936d66f6a032555974a0453010f08f345d0f6
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250519"
---
# <a name="oid_qos_offload_sq_stats"></a>OID_QOS_OFFLOAD_SQ_STATS

过量驱动程序发出 OID_QOS_OFFLOAD_SQ_STATS 的 OID 方法请求，以获取所有计划程序队列的列表 (SQs) 及其状态计数器，这些队列当前存在于微型端口适配器上。

成功从 OID 查询请求返回后， [**NDIS_OID_REQUEST**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS_QOS_SQ_ARRAY**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-ndis_qos_sq_parameters_enum_array)结构的指针。 数组的每个元素都是一个 [**NDIS_QOS_SQ_STATS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-ndis_qos_sq_stats) 的结构。

如果 OID 查询的 **NDIS_OID_REQUEST** 缓冲区包含有效的 VPortId，则返回的统计信息特定于指定的 vPort。 否则，统计信息会指定与每个 SQ 关联的所有 vPorts 的总统计信息。

## <a name="remarks"></a>备注

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理微型端口驱动程序的 OID_QOS_OFFLOAD_SQ_STATS 的 OID 方法请求，并返回以下状态代码之一。

|状态代码|说明|
|--- |--- |
|NDIS_STATUS_SUCCESS|OID 请求已成功完成。|
|NDIS_STATUS_NOT_SUPPORTED|微型端口驱动程序不支持 NDIS QoS 接口。|
|NDIS_STATUS_INVALID_PARAMETER|**InformationBuffer** 的长度小于 NDIS_SIZEOF_QOS_SQ_ARRAY_REVISION_1。|
|NDIS_STATUS_BUFFER_TOO_SHORT|信息缓冲区的长度不足以获得返回的数据。|
|NDIS_STATUS_Xxx|由于其他原因，请求失败。|

 

## <a name="requirements"></a>要求

|要求|值|
|--- |--- |
|Version|在 NDIS 6.85 和更高版本中受支持。|
|标题|Ntddndis (包含 Ndis .h) |

## <a name="see-also"></a>请参阅

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS_QOS_SQ_PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-ndis_qos_sq_parameters)

[**NDIS_QOS_SQ_ARRAY**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-ndis_qos_sq_parameters_enum_array)

[**NDIS_QOS_SQ_STATS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-ndis_qos_sq_stats)
 
