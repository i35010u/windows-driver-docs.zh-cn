---
title: OID_QOS_OFFLOAD_DELETE_SQ
description: OID_QOS_OFFLOAD_DELETE_SQ 在微型端口适配器上删除计划程序队列 (SQ) 的驱动程序问题。
ms.assetid: ''
ms.date: 10/30/2020
keywords: -从 Windows Vista 开始 OID_QOS_OFFLOAD_DELETE_SQ 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 61847f6cb24b86626a45e5b2749f50a319bd325f
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250522"
---
# <a name="oid_qos_offload_delete_sq"></a>OID_QOS_OFFLOAD_DELETE_SQ

过量驱动程序发出 OID 设置 OID_QOS_OFFLOAD_DELETE_SQ 的请求，以便在微型端口适配器上 (SQ) 删除计划程序队列。 调用方应将 [**NDIS_OID_REQUEST**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员设置为包含指向 **NDIS_QOS_SQ_ID** 的指针。

## <a name="remarks"></a>备注

调用方必须确保在删除之前没有任何资源主动引用此 SQ。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理微型端口驱动程序的 OID_QOS_OFFLOAD_DELETE_SQ OID 集请求，并返回以下状态代码之一。

|状态代码|说明|
|--- |--- |
|NDIS_STATUS_SUCCESS|OID 请求已成功完成。|
|NDIS_STATUS_NOT_SUPPORTED|微型端口驱动程序不支持 NDIS QoS 接口。|
|NDIS_STATUS_Xxx|由于其他原因，请求失败。|

 
## <a name="requirements"></a>要求

|要求|值|
|--- |--- |
|Version|在 NDIS 6.85 和更高版本中受支持。|
|标题|Ntddndis (包含 Ndis .h) |

## <a name="see-also"></a>请参阅

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[OID_QOS_OFFLOAD_CREATE_SQ](oid-qos-offload-create-sq.md)

[OID_QOS_OFFLOAD_UPDATE_SQ](oid-qos-offload-update-sq.md)

