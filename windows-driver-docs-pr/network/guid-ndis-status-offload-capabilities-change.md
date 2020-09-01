---
title: GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE GUID。
ms.assetid: f1daadff-a564-4308-82cd-525a1dae866a
keywords:
- GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE，WDK GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0742ab6def51a8065a4f69c88feb4906908598c3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218099"
---
# <a name="guid_ndis_status_offload_capabilities_change"></a>GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE

GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE 事件 GUID 表示 NDIS 端口或微型端口适配器的卸载特性发生了更改。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

微型端口驱动程序使用 [NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md) 状态指示通知 NDIS 和过量驱动程序已更改任务卸载功能。

当微型端口驱动程序指示任务卸载更改时，NDIS 会将状态指示转换为 WMI 客户端的 WMI GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE 事件。

具有 GUID 的 NDIS 提供的数据缓冲区包含后跟[NDIS_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构的[NDIS_WMI_EVENT_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)结构。

有关任务卸载功能的详细信息，请参阅 [NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md) 和 [OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)。