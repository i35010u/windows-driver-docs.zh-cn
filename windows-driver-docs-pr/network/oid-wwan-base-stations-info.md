---
title: OID_WWAN_BASE_STATIONS_INFO
description: OID_WWAN_BASE_STATIONS_INFO
ms.assetid: 041CFD25-7CEA-4041-B723-E42FB8189461
keywords:
- MB 基站信息 OID，移动宽带基站信息 OID，移动宽带微型端口驱动程序基站信息 OID
ms.date: 08/21/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe18d8c132fc4cb13750f12024d58a96c59e4597
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843874"
---
# <a name="oid_wwan_base_stations_info"></a>OID_WWAN_BASE_STATIONS_INFO

OID_WWAN_BASE_STATIONS_INFO 检索有关调制解调器已知的服务和相邻单元格的信息。 有关手机网络基站信息查询的详细信息，请参阅[MB 基站信息查询支持](mb-base-stations-information-query-support.md)。

对于查询请求，OID_WWAN_BASE_STATIONS_INFO 使用[NDIS_WWAN_BASE_STATIONS_INFO_REQ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info_req)结构，后者又包含用于指定单元信息的各个方面的[WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_base_stations_info)结构，如最大值要在响应中发送的邻居单元格度量的数目。 调制解调器小型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回给原始请求，然后再发送包含 NDIS_ 的[NDIS_STATUS_WWAN_BASE_STATIONS_INFO](ndis-status-wwan-base-stations-info.md)通知[WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)结构，后者又包含一个[WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_base_stations_info)结构，该结构提供有关服务和邻居基站的信息。

设置请求不适用。

未经请求的事件不适用。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows 10 版本 1709 |
| 标头 | Ntddndis （包括 Ndis .h） |

## <a name="see-also"></a>另请参阅

[NDIS_WWAN_BASE_STATIONS_INFO_REQ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info_req)

[NDIS_STATUS_WWAN_BASE_STATIONS_INFO](ndis-status-wwan-base-stations-info.md)

[NDIS_WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_base_stations_info)

[WWAN_BASE_STATIONS_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_base_stations_info)

[MB 基站信息查询支持](mb-base-stations-information-query-support.md)

