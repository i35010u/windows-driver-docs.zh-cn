---
title: GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX GUID。
ms.assetid: 34839471-5b3b-4a95-a610-bc35e7774c14
keywords:
- GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX，WDK GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9deabb69beaeb5691c628e9f48a48dfffc6c4323
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842278"
---
# <a name="guid_ndis_status_media_specific_indication_ex"></a>GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX

GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX 事件 GUID 指示特定于介质的状态。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

当微型端口驱动程序指示特定于媒体的状态时，NDIS 会将状态指示转换为 wmi 客户端的 WMI GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX 指示。

微型端口驱动程序通过将[NdisMIndicateStatusEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)函数与*StatusIndication*参数指向的[NDIS_STATUS_INDICATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusCode**成员一起调用，使特定于媒体的状态指示设置为 NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX。 此结构的**StatusBuffer**成员指向驱动程序分配的缓冲区，该缓冲区包含特定于**StatusCode**中标识的状态指示的格式的数据。

根据特定于介质的指示类型，GUID 标头后面可以跟特定于媒体特定指示的数据。 使用此 GUID 提供的 NDIS 提供的数据缓冲区包含[NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)结构，后跟媒体特定的数据（如果有）。

