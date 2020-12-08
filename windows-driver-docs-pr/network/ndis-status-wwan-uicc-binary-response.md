---
title: NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE 通知来通知移动宽带 (MB) 服务，以了解以前的 OID_WWAN_UICC_ACCESS_BINARY 查询请求是否完成。
ms.date: 04/10/2019
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE 的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: f348aa4d60b364d987b7b50bed176fb4440ed972
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840009"
---
# <a name="ndis_status_wwan_uicc_binary_response"></a>NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE

微型端口驱动程序使用 **NDIS_STATUS_WWAN_UICC_BINARY_RESPONSE** 通知来通知移动宽带 (MB) 服务与先前 [OID_WWAN_UICC_ACCESS_BINARY](oid-wwan-uicc-access-binary.md) 查询或设置请求的完成有关。

未经请求的事件不适用。

此通知使用 [**NDIS_WWAN_UICC_RESPONSE**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1903 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>请参阅

[MB UICC 应用程序和文件系统访问权限](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_ACCESS_BINARY](oid-wwan-uicc-access-binary.md)

[**NDIS_WWAN_UICC_RESPONSE**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_response)
