---
title: GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE GUID。
ms.assetid: f1daadff-a564-4308-82cd-525a1dae866a
keywords:
- GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE，WDK GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12f757fbd13f7ea62051f8ee7bf37b92867c479e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369665"
---
# <a name="guidndisstatusoffloadcapabilitieschange"></a>GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE

GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE 事件 GUID 表示已被卸载特征的 NDIS 端口或微型端口适配器中的更改。 NDIS 6.0 及更高版本支持此 WMI GUID。

微型端口驱动程序使用[NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)状态指示通知 NDIS 和基础驱动程序已在任务更改卸载功能。

当微型端口驱动程序指示任务卸载更改时，NDIS 将转换为 WMI GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE 事件的 WMI 客户端的状态指示。

包含的数据缓冲区的 NDIS 提供具有 GUID [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_event_header)结构，后跟[NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构。

有关任务卸载功能的详细信息，请参阅[NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)并[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)。

