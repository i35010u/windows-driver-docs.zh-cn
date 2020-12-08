---
title: NDIS_STATUS_WWAN_SAR_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SAR_CONFIG 通知来通知移动宽带 (MB) 服务与先前 OID_WWAN_SAR_CONFIG 查询或设置请求的完成有关。
ms.date: 08/17/2018
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SAR_CONFIG 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3ecc6c70628b17d2640b475c8f1a271229856eb2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802319"
---
# <a name="ndis_status_wwan_sar_config"></a>NDIS_STATUS_WWAN_SAR_CONFIG

微型端口驱动程序使用 **NDIS_STATUS_WWAN_SAR_CONFIG** 通知来通知移动宽带 (MB) 服务与先前 [OID_WWAN_SAR_CONFIG](oid-wwan-sar-config.md) 查询或设置请求的完成有关。

未经请求的事件不适用。

此通知使用 [**NDIS_WWAN_SAR_CONFIG_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1703 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>请参阅

[MB SAR 平台支持](./mb-sar-platform-support.md)

[OID_WWAN_SAR_CONFIG](oid-wwan-sar-config.md)

[**NDIS_WWAN_SAR_CONFIG_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)
