---
title: NDIS_STATUS_WWAN_BASE_STATIONS_INFO
description: NDIS_STATUS_WWAN_BASE_STATIONS_INFO
ms.assetid: 57E22B53-5ECC-4B4C-8A98-C1125314868B
keywords:
- NDIS_STATUS_WWAN_BASE_STATIONS_INFO，基站信息查询状态通知，移动宽带基本工作站信息查询状态通知，MB 基站信息查询状态通知
ms.date: 08/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: 072277dc697616ed62257a0a291e7af5d76a1d3d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842105"
---
# <a name="ndis_status_wwan_base_stations_info"></a>NDIS_STATUS_WWAN_BASE_STATIONS_INFO

NDIS_STATUS_WWAN_BASE_STATIONS_INFO 通知由调制解调器的小型端口驱动程序发送，以响应[OID_WWAN_BASE_STATIONS_INFO](oid-wwan-base-stations-info.md)查询请求，以向 MB 主机提供有关服务和邻居基站的信息。

此通知使用[NDIS_WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)结构。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows 10 版本 1709 |
| 标头 | Ndis。h |

## <a name="see-also"></a>另请参阅

[OID_WWAN_BASE_STATIONS_INFO](oid-wwan-base-stations-info.md)

[NDIS_WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)

[MB 基站信息查询操作](mb-base-stations-information-query-support.md)

