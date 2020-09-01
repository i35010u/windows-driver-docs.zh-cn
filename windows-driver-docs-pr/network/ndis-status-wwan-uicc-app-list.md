---
title: NDIS_STATUS_WWAN_UICC_APP_LIST
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_UICC_APP_LIST 通知来通知移动宽带 (MB) 服务，以了解以前的 OID_WWAN_UICC_APP_LIST 查询请求是否完成。
ms.assetid: D18BA7C8-5CEC-4DF6-BB5A-C8F65E1911A5
ms.date: 04/08/2019
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_UICC_APP_LIST 的网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e7a0f273ffbc5d979a135cf3c4c358993612845a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211683"
---
# <a name="ndis_status_wwan_uicc_app_list"></a>NDIS_STATUS_WWAN_UICC_APP_LIST

微型端口驱动程序使用 **NDIS_STATUS_WWAN_UICC_APP_LIST** 通知来通知移动宽带 (MB) 服务，以了解以前的 [OID_WWAN_UICC_APP_LIST](oid-wwan-uicc-app-list.md) 查询请求是否完成。

未经请求的事件不适用。

此通知使用 [**NDIS_WWAN_UICC_APP_LIST**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1903 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>另请参阅

[MB UICC 应用程序和文件系统访问权限](mb-uicc-application-and-file-system-access.md)

[OID_WWAN_UICC_APP_LIST](oid-wwan-uicc-app-list.md)

[**NDIS_WWAN_UICC_APP_LIST**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_app_list)