---
title: OID_QOS_OFFLOAD_UPDATE_SQ
description: 过量驱动程序发出 OID 设置 OID_QOS_OFFLOAD_UPDATE_SQ 的请求，以更新微型端口适配器上 (SQ) 的计划程序队列。
ms.assetid: ''
ms.date: 10/30/2020
keywords: -从 Windows Vista 开始 OID_QOS_OFFLOAD_UPDATE_SQ 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2cb4e034df4ec3141443a98baa6e814142fb5fae
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250518"
---
# <a name="oid_qos_offload_update_sq"></a>OID_QOS_OFFLOAD_UPDATE_SQ

过量驱动程序发出 OID 设置 OID_QOS_OFFLOAD_UPDATE_SQ 的请求，以更新微型端口适配器上 (SQ) 的计划程序队列。 调用方应将 [**NDIS_OID_REQUEST**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员设置为包含指向 [**NDIS_QOS_SQ_PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-ndis_qos_sq_parameters)结构的指针。

调用方应将 **NDIS_QOS_SQ_PARAMETERS** 的 " **SqId** " 字段设置为它要更新的 SQ 的当前 sq ID。 调用方应将其余字段设置为它在此 SQ 上所需的完整参数集，但不能更新的 **SqType** 字段除外。

## <a name="remarks"></a>备注

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理微型端口驱动程序的 OID_QOS_OFFLOAD_UPDATE_SQ OID 集请求，并返回以下状态代码之一。

|状态代码|说明|
|--- |--- |
|NDIS_STATUS_SUCCESS|OID 请求已成功完成。|
|NDIS_STATUS_NOT_SUPPORTED|微型端口驱动程序不支持 NDIS QoS 接口。|
|NDIS_STATUS_INVALID_PARAMETER|**InformationBuffer** 的长度小于 NDIS_SIZEOF_QOS_SQ_PARAMETERS_REVISION_1。|
|NDIS_STATUS_Xxx|由于其他原因，请求失败。|

 

## <a name="requirements"></a>要求

|要求|值|
|--- |--- |
|Version|在 NDIS 6.85 和更高版本中受支持。|
|标题|Ntddndis (包含 Ndis .h) |

## <a name="see-also"></a>请参阅

[**NDIS \_ OID \_ 请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS_QOS_SQ_PARAMETERS**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-ndis_qos_sq_parameters)

[OID_QOS_OFFLOAD_CREATE_SQ](oid-qos-offload-create-sq.md)

[OID_QOS_OFFLOAD_DELETE_SQ](oid-qos-offload-delete-sq.md)


 
