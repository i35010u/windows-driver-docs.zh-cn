---
title: GUID_NDIS_STATUS_LINK_STATE
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_STATUS_LINK_STATE GUID。
keywords:
- GUID_NDIS_STATUS_LINK_STATE，WDK GUID_NDIS_STATUS_LINK_STATE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71bf11628f5b669ce1a37f67d75140369b4288fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799389"
---
# <a name="guid_ndis_status_link_state"></a>GUID_NDIS_STATUS_LINK_STATE

GUID_NDIS_STATUS_LINK_STATE 事件 GUID 指示微型端口适配器的链接状态发生了更改。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

微型端口驱动程序使用 [NDIS_STATUS_LINK_STATE](ndis-status-link-state.md) 状态指示通知 NDIS 和过量驱动程序已更改链接状态。

当微型端口驱动程序指示链接状态更改时，NDIS 会将状态指示转换为 WMI 客户端的 WMI GUID_NDIS_STATUS_LINK_STATE 事件。

具有 GUID 的 NDIS 提供的数据缓冲区包含后跟[NDIS_LINK_STATE](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构的[NDIS_WMI_EVENT_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)结构。 **NDIS_LINK_STATE** 结构指定介质的物理状态。

有关链接状态的详细信息，请参阅 [OID_GEN_LINK_STATE](oid-gen-link-state.md) 和 [NDIS_STATUS_LINK_STATE](ndis-status-link-state.md)。
