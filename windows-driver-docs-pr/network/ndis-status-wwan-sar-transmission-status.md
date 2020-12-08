---
title: NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS 通知来通知移动宽带 (MB) 服务与先前 OID_WWAN_SAR_TRANSMISSION_STATUS 查询或设置请求的完成有关。
ms.date: 08/20/2018
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cde302f5742ef28dc806df9ac0fcdea7b04ad1f5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818865"
---
# <a name="ndis_status_wwan_sar_transmission_status"></a>NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS

微型端口驱动程序使用 **NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS** 通知来通知移动宽带 (MB) 服务与先前 [OID_WWAN_SAR_TRANSMISSION_STATUS](oid-wwan-sar-transmission-status.md) 查询或设置请求的完成有关。

当活动无线 (OTA) 通道发生变化时，将发送未经请求的事件。 例如，如果调制解调器开始上传数据包数据，则需要在使用网络数据通道时设置上行通道，以便能够上传有效负载。 这会触发向操作系统提供通知。

此通知使用 [**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_TRANSMISSION_STATUS_info) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1703 **头**： Ntddndis (包括 Ndis .h) 

## <a name="see-also"></a>请参阅

[MB SAR 平台支持](./mb-sar-platform-support.md)

[OID_WWAN_SAR_TRANSMISSION_STATUS](oid-wwan-sar-transmission-status.md)

[**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info)
