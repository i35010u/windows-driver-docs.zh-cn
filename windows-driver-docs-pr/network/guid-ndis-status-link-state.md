---
title: GUID_NDIS_STATUS_LINK_STATE
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_STATUS_LINK_STATE GUID。
ms.assetid: 7f56d211-14c7-4b8b-8d1c-ee7836b7b70a
keywords:
- GUID_NDIS_STATUS_LINK_STATE，WDK GUID_NDIS_STATUS_LINK_STATE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4d8cee1684b7acfe1a199a218371159db995106
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218105"
---
# <a name="guid_ndis_status_link_state"></a>GUID_NDIS_STATUS_LINK_STATE

GUID_NDIS_STATUS_LINK_STATE 事件 GUID 指示微型端口适配器的链接状态发生了更改。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

微型端口驱动程序使用 [NDIS_STATUS_LINK_STATE](ndis-status-link-state.md) 状态指示通知 NDIS 和过量驱动程序已更改链接状态。

当微型端口驱动程序指示链接状态更改时，NDIS 会将状态指示转换为 WMI 客户端的 WMI GUID_NDIS_STATUS_LINK_STATE 事件。

具有 GUID 的 NDIS 提供的数据缓冲区包含后跟[NDIS_LINK_STATE](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构的[NDIS_WMI_EVENT_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)结构。 **NDIS_LINK_STATE**结构指定介质的物理状态。

有关链接状态的详细信息，请参阅 [OID_GEN_LINK_STATE](oid-gen-link-state.md) 和 [NDIS_STATUS_LINK_STATE](ndis-status-link-state.md)。