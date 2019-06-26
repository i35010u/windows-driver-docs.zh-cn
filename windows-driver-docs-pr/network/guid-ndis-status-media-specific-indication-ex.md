---
title: GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX GUID。
ms.assetid: 34839471-5b3b-4a95-a610-bc35e7774c14
keywords:
- GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX，WDK GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdc108e8d1d2b64e00215c15b7d3edc3152b6b2f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382684"
---
# <a name="guidndisstatusmediaspecificindicationex"></a>GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX

GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX 事件 GUID 表示特定于媒体的状态。 NDIS 6.0 及更高版本支持此 WMI GUID。

当微型端口驱动程序指示特定于媒体的状态时，NDIS 将转换为 WMI 客户端会向 WMI GUID_NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX 指示状态的指示。

微型端口驱动程序通过调用做出特定于媒体的状态指示[NdisMIndicateStatusEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)起作用**StatusCode**的成员[NDIS_STATUS_INDICATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构的*StatusIndication*参数所指向要设置为 NDIS_STATUS_MEDIA_SPECIFIC_INDICATION_EX。 **StatusBuffer**此结构的成员将指向包含特定于中标识的状态指示的格式中的数据的驱动程序分配的缓冲区**StatusCode**。

根据特定于媒体的指示的类型，GUID 标头可以跟数据特定于特定于媒体的指示。 NDIS 提供具有此 GUID 的数据缓冲区包含[NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_event_header)后跟媒体特定的数据，如果任何的结构。

