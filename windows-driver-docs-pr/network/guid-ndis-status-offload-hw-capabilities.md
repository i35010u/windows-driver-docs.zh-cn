---
title: GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES GUID。
ms.assetid: 6f5e11c1-4fa0-4a9b-90f3-85a3cb8b8878
keywords:
- GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES，WDK GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 296c738742425851722d1e8ad6910c2bd4e10aea
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369659"
---
# <a name="guidndisstatusoffloadhwcapabilities"></a>GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES

GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES 事件 GUID 表示已与的 NDIS 端口或微型端口适配器相关联的硬件的卸载特征中的更改。 添加或删除与 MUX 中间驱动程序相关联的硬件，通常反映了硬件更改。 NDIS 6.0 及更高版本支持此 WMI GUID。

MUX 驱动程序使用的中间[NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES](ndis-status-task-offload-hardware-capabilities.md)状态指示通知 NDIS 和基础驱动程序已在任务更改卸载功能。

当驱动程序指示任务卸载硬件发生变化时，NDIS 将转换为 WMI GUID_NDIS_STATUS_OFFLOAD_HW_CAPABILITIES 事件的 WMI 客户端的状态指示。

包含的数据缓冲区的 NDIS 提供具有 GUID [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_event_header)结构，后跟[NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构。

有关任务卸载功能的详细信息，请参阅[NDIS_STATUS_TASK_OFFLOAD_HARDWARE_CAPABILITIES](ndis-status-task-offload-hardware-capabilities.md)并[OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES](oid-tcp-offload-hardware-capabilities.md)。

