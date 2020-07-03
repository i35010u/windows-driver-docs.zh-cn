---
title: NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE 通知来通知移动宽带（MB）服务完成了上一个 OID_WWAN_UICC_ACCESS_RECORD 查询请求。
ms.assetid: 5F729855-1056-43D3-BEF8-A2A2D4CA56CB
ms.date: 04/10/2019
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE 的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 38c3944223468723a4baa626ccc54fcf89e340f5
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916630"
---
# <a name="ndis_status_wwan_uicc_record_response"></a>NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE

微型端口驱动程序使用**NDIS_STATUS_WWAN_UICC_RECORD_RESPONSE**通知来通知移动宽带（MB）服务完成了上一个[OID_WWAN_UICC_ACCESS_RECORD](oid-wwan-uicc-access-record.md)查询或设置请求。

未经请求的事件不适用。

此通知使用[**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1903**头**： Ntddndis （包括 Ndis .h）

## <a name="see-also"></a>另请参阅

[MB UICC 应用程序和文件系统访问权限](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_ACCESS_RECORD](oid-wwan-uicc-access-record.md)

[**NDIS_WWAN_UICC_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)
