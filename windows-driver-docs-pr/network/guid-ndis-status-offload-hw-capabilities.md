---
title: GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES GUID。
keywords:
- GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES，WDK GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b20131458eec149af4328119590cf15a428e84b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782269"
---
# <a name="guid_ndis_status_offload_hw_capabilities"></a>GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES

GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES 事件 GUID 表示与 NDIS 端口或微型端口适配器关联的硬件的卸载特性发生了变化。 硬件更改通常会反映添加或删除与 MUX 中间驱动程序关联的硬件。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

MUX 中间驱动程序使用 [NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES](ndis-status-task-offload-hardware-capabilities.md) 状态指示通知 NDIS 和过量驱动程序已更改任务卸载功能。

当驱动程序指示任务卸载硬件更改时，NDIS 会将状态指示转换为 WMI 客户端的 WMI GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES 事件。

具有 GUID 的 NDIS 提供的数据缓冲区包含后跟[NDIS_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构的[NDIS_WMI_EVENT_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)结构。

有关任务卸载功能的详细信息，请参阅 [NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES](ndis-status-task-offload-hardware-capabilities.md) 和 [OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES](oid-tcp-offload-hardware-capabilities.md)。
