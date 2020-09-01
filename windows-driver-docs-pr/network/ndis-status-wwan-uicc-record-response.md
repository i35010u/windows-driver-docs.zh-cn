---
title: NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE 通知来通知移动宽带 (MB) 服务，以了解以前的 OID_WWAN_UICC_ACCESS_RECORD 查询请求是否完成。
ms.assetid: 5F729855-1056-43D3-BEF8-A2A2D4CA56CB
ms.date: 04/10/2019
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE 的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c5ac811a31a28a2261653eaf0a504aec4a9ac75d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211677"
---
# <a name="ndis_status_wwan_uicc_record_response"></a>NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE

微型端口驱动程序使用 **NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE** 通知来通知移动宽带 (MB) 服务与先前 [OID_WWAN_UICC_ACCESS_RECORD](oid-wwan-uicc-access-record.md) 查询或设置请求的完成有关。

未经请求的事件不适用。

此通知使用 [**NDIS_WWAN_UICC_RESPONSE**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1903 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>另请参阅

[MB UICC 应用程序和文件系统访问权限](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_ACCESS_RECORD](oid-wwan-uicc-access-record.md)

[**NDIS_WWAN_UICC_RESPONSE**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)