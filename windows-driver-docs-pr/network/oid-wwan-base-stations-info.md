---
title: OID_WWAN_BASE_STATIONS_INFO
description: OID_WWAN_BASE_STATIONS_INFO
ms.assetid: 041CFD25-7CEA-4041-B723-E42FB8189461
keywords:
- MB 基站信息 OID，移动宽带的基站信息 OID，移动宽带的微型端口驱动程序基站信息 OID
ms.date: 08/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6be46c88322efaf928477bf6f94fc97f0f35d84e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362872"
---
# <a name="oidwwanbasestationsinfo"></a>OID_WWAN_BASE_STATIONS_INFO

OID_WWAN_BASE_STATIONS_INFO 检索有关服务和相邻单元格到调制解调器的已知信息。 有关手机基站信息查询的详细信息，请参阅[MB 基站配合信息的查询支持](mb-base-stations-information-query-support.md)。

对于查询请求，使用 OID_WWAN_BASE_STATIONS_INFO [NDIS_WWAN_BASE_STATIONS_INFO_REQ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info_req)结构，其中又包含[WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_base_stations_info)结构，它指定的方面单元格的信息，例如相邻单元格度量，若要在响应中发送的最大数目。 调制解调器微型端口驱动程序必须查询请求进行异步处理，最初在更高版本发送之前对原始请求返回 NDIS_STATUS_INDICATION_REQUIRED [NDIS_STATUS_WWAN_BASE_STATIONS_INFO](ndis-status-wwan-base-stations-info.md)通知包含[NDIS_WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)结构，其中又包含[WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_base_stations_info)结构，它提供了有关提供邻近的基本信息。工作站。

不适用集发出的请求。

未经请求的事件不适用。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows 10 版本 1709 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[NDIS_WWAN_BASE_STATIONS_INFO_REQ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info_req)

[NDIS_STATUS_WWAN_BASE_STATIONS_INFO](ndis-status-wwan-base-stations-info.md)

[NDIS_WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)

[WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_base_stations_info)

[MB 基站信息查询支持](mb-base-stations-information-query-support.md)

