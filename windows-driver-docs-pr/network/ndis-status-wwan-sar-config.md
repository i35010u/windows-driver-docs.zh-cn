---
title: NDIS_STATUS_WWAN_SAR_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SAR_CONFIG 通知来通知移动宽带（MB）服务完成了上一个 OID_WWAN_SAR_CONFIG 查询或设置请求。
ms.assetid: 50DAEFAB-E86A-41EA-A237-802AD8F83BB2
ms.date: 08/17/2018
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SAR_CONFIG 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7118d8e8050b4d1a12a7e919fd0d81bf15ca2ce2
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918017"
---
# <a name="ndis_status_wwan_sar_config"></a>NDIS_STATUS_WWAN_SAR_CONFIG

微型端口驱动程序使用**NDIS_STATUS_WWAN_SAR_CONFIG**通知来通知移动宽带（MB）服务完成了上一个[OID_WWAN_SAR_CONFIG](oid-wwan-sar-config.md)查询或设置请求。

未经请求的事件不适用。

此通知使用[**NDIS_WWAN_SAR_CONFIG_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1703**头**： Ntddndis （包括 Ndis .h）

## <a name="see-also"></a>另请参阅

[MB SAR 平台支持](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)

[OID_WWAN_SAR_CONFIG](oid-wwan-sar-config.md)

[**NDIS_WWAN_SAR_CONFIG_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)
