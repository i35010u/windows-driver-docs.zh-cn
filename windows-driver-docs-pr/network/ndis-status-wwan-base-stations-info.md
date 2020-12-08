---
title: NDIS_STATUS_WWAN_BASE_STATIONS_INFO
description: NDIS_STATUS_WWAN_BASE_STATIONS_INFO
keywords:
- NDIS_STATUS_WWAN_BASE_STATIONS_INFO，基站信息查询状态通知，移动宽带基本工作站信息查询状态通知，MB 基站信息查询状态通知
ms.date: 08/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bdeafb83f8a48f8e7e933fab9d8f26ed354dc1f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839475"
---
# <a name="ndis_status_wwan_base_stations_info"></a>NDIS_STATUS_WWAN_BASE_STATIONS_INFO

NDIS_STATUS_WWAN_BASE_STATIONS_INFO 通知由调制解调器端口驱动程序发送以响应 [OID_WWAN_BASE_STATIONS_INFO](oid-wwan-base-stations-info.md) 的查询请求，以向 MB 主机提供服务和邻近的基站的相关信息。

此通知使用 [NDIS_WWAN_BASE_STATIONS_INFO](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info) 结构。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1709 **头**： Ndis。h

## <a name="see-also"></a>请参阅

[OID_WWAN_BASE_STATIONS_INFO](oid-wwan-base-stations-info.md)

[NDIS_WWAN_BASE_STATIONS_INFO](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)

[MB 基站信息查询操作](mb-base-stations-information-query-support.md)
