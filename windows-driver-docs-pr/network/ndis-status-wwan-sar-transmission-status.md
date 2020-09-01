---
title: NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS 通知来通知移动宽带 (MB) 服务与先前 OID_WWAN_SAR_TRANSMISSION_STATUS 查询或设置请求的完成有关。
ms.assetid: 0F04AC31-A16F-4E6A-A5FF-A69574A300A1
ms.date: 08/20/2018
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8829c738a9f89255f4c5e31ba4d45024ae1d7717
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211697"
---
# <a name="ndis_status_wwan_sar_transmission_status"></a>NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS

微型端口驱动程序使用 **NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS** 通知来通知移动宽带 (MB) 服务与先前 [OID_WWAN_SAR_TRANSMISSION_STATUS](oid-wwan-sar-transmission-status.md) 查询或设置请求的完成有关。

当活动无线 (OTA) 通道发生变化时，将发送未经请求的事件。 例如，如果调制解调器开始上传数据包数据，则需要在使用网络数据通道时设置上行通道，以便能够上传有效负载。 这会触发向操作系统提供通知。

此通知使用 [**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_TRANSMISSION_STATUS_info) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1703 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>另请参阅

[MB SAR 平台支持](./mb-sar-platform-support.md)

[OID_WWAN_SAR_TRANSMISSION_STATUS](oid-wwan-sar-transmission-status.md)

[**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info)