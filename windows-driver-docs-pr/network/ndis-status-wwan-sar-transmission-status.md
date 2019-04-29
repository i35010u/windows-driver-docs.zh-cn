---
title: NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS 通知来通知关于完成的上一个 OID_WWAN_SAR_TRANSMISSION_STATUS 查询或一组请求的移动宽带 (MB) 服务。
ms.assetid: 0F04AC31-A16F-4E6A-A5FF-A69574A300A1
ms.date: 08/20/2018
keywords: -NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7b8250b6494324f0f13f1eb838ed3d39ca27c637
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372210"
---
# <a name="ndisstatuswwansartransmissionstatus"></a>NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS

微型端口驱动程序使用**NDIS_STATUS_WWAN_SAR_TRANSMISSION_STATUS**通知来通知关于完成的上一次移动宽带 (MB) 服务[OID_WWAN_SAR_TRANSMISSION_STATUS](oid-wwan-sar-transmission-status.md)查询或设置请求。

未经请求的事件发送到活动的无线 (OTA) 通道的更改时。 例如，如果调制解调器开始上传数据包数据，它所需设置上行通道时它使用的网络数据通道，以便它可以上传有效负载。 这将触发该通知可提供给操作系统。

使用此通知[ **NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_TRANSMISSION_STATUS_info)结构。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10 版本 1703 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[MB 特别行政区平台支持](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)

[OID_WWAN_SAR_TRANSMISSION_STATUS](oid-wwan-sar-transmission-status.md)

[**NDIS_WWAN_SAR_TRANSMISSION_STATUS_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_transmission_status_info)
