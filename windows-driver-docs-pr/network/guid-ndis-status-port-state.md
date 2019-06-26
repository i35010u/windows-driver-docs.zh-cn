---
title: GUID_NDIS_STATUS_PORT_STATE
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_STATUS_PORT_STATE GUID。
ms.assetid: c657eef6-eb80-4715-9d60-0d2dde403300
keywords:
- GUID_NDIS_STATUS_PORT_STATE，WDK GUID_NDIS_STATUS_PORT_STATE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7413087988a808903d0557500d3e8f09ef405661
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366639"
---
# <a name="guidndisstatusportstate"></a>GUID_NDIS_STATUS_PORT_STATE

GUID_NDIS_STATUS_PORT_STATE 事件 GUID 表示的 NDIS 端口状态的更改。 NDIS 6.0 及更高版本支持此 WMI GUID。

支持 NDIS 端口使用的微型端口驱动程序[NDIS_STATUS_PORT_STATE](ndis-status-port-state.md)状态指示，指示在 NDIS 端口的状态更改。

当微型端口驱动程序指示端口状态更改时，NDIS 将转换为 WMI GUID_NDIS_STATUS_PORT_STATE 事件的 WMI 客户端的状态指示。

NDIS 提供具有此 GUID 的数据缓冲区包含[NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_event_header)结构，后跟[NDIS_PORT_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state)结构。

有关端口状态的详细信息，请参阅[OID_GEN_PORT_STATE](oid-gen-port-state.md)。

