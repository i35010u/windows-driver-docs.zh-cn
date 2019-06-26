---
title: NDIS_STATUS_WWAN_BASE_STATIONS_INFO
description: NDIS_STATUS_WWAN_BASE_STATIONS_INFO
ms.assetid: 57E22B53-5ECC-4B4C-8A98-C1125314868B
keywords:
- NDIS_STATUS_WWAN_BASE_STATIONS_INFO，基站配合信息查询状态通知、 移动宽带的基站信息查询状态通知、 MB 基站信息查询状态通知
ms.date: 08/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: bde60bc98636c34ab76de1dab49cfcb844cb4cab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375189"
---
# <a name="ndisstatuswwanbasestationsinfo"></a>NDIS_STATUS_WWAN_BASE_STATIONS_INFO

NDIS_STATUS_WWAN_BASE_STATIONS_INFO 通知发送到响应中的调制解调器微型端口驱动程序[OID_WWAN_BASE_STATIONS_INFO](oid-wwan-base-stations-info.md) MB 主机提供关于服务和相邻的信息的查询请求基站。

使用此通知[NDIS_WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)结构。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows 10 版本 1709 |
| Header | Ndis.h |

## <a name="see-also"></a>请参阅

[OID_WWAN_BASE_STATIONS_INFO](oid-wwan-base-stations-info.md)

[NDIS_WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)

[MB 基站配合的查询操作的信息](mb-base-stations-information-query-support.md)

