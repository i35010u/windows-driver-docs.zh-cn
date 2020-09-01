---
title: OID_WWAN_LTE_ATTACH_STATUS
description: OID_WWAN_LTE_ATTACH_STATUS 用于通知操作系统上次使用的 LTE 附加上下文。
ms.assetid: 394650CF-5410-40C6-8749-D941DF68D303
ms.date: 08/23/2018
keywords: -从 Windows Vista 开始 OID_WWAN_LTE_ATTACH_STATUS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cbd2ae98bdcd52c9b951841fa7f5ec6026026b01
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210099"
---
# <a name="oid_wwan_lte_attach_status"></a>OID_WWAN_LTE_ATTACH_STATUS

OID_WWAN_LTE_ATTACH_STATUS 用于通知操作系统上次使用的默认 LTE 附加上下文。

微型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回到原始请求，然后再发送 [NDIS_STATUS_WWAN_LTE_ATTACH_STATUS](ndis-status-wwan-lte-attach-status.md) 通知，其中包含描述上次使用的默认 LTE 附加上下文的 [**NDIS_WWAN_LTE_ATTACH_STATUS**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_status) 结构。

设置请求不适用。

## <a name="remarks"></a>备注

有关使用此 OID 的详细信息，请参阅 [MBIM_CID_MS_LTE_ATTACH_STATUS](mb-lte-attach-operations.md)。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1703 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>另请参阅

[MB LTE 附加操作](mb-lte-attach-operations.md)

[NDIS_STATUS_WWAN_LTE_ATTACH_STATUS](ndis-status-wwan-lte-attach-status.md)

[**NDIS_WWAN_LTE_ATTACH_STATUS**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_lte_attach_status)