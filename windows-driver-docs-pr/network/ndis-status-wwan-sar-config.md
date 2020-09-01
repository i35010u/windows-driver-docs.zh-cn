---
title: NDIS_STATUS_WWAN_SAR_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SAR_CONFIG 通知来通知移动宽带 (MB) 服务与先前 OID_WWAN_SAR_CONFIG 查询或设置请求的完成有关。
ms.assetid: 50DAEFAB-E86A-41EA-A237-802AD8F83BB2
ms.date: 08/17/2018
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SAR_CONFIG 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fb98021ab7da42bae7c656376f8053de7a607c0e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211699"
---
# <a name="ndis_status_wwan_sar_config"></a>NDIS_STATUS_WWAN_SAR_CONFIG

微型端口驱动程序使用 **NDIS_STATUS_WWAN_SAR_CONFIG** 通知来通知移动宽带 (MB) 服务与先前 [OID_WWAN_SAR_CONFIG](oid-wwan-sar-config.md) 查询或设置请求的完成有关。

未经请求的事件不适用。

此通知使用 [**NDIS_WWAN_SAR_CONFIG_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1703 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>另请参阅

[MB SAR 平台支持](./mb-sar-platform-support.md)

[OID_WWAN_SAR_CONFIG](oid-wwan-sar-config.md)

[**NDIS_WWAN_SAR_CONFIG_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)