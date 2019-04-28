---
title: GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE GUID。
ms.assetid: f1daadff-a564-4308-82cd-525a1dae866a
keywords:
- GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE，WDK GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fdd85a78851c5df5578d018e7ab07f48023009f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349869"
---
# <a name="guidndisstatusoffloadcapabilitieschange"></a>GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE

GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE 事件 GUID 表示已被卸载特征的 NDIS 端口或微型端口适配器中的更改。 NDIS 6.0 及更高版本支持此 WMI GUID。

微型端口驱动程序使用[NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)状态指示通知 NDIS 和基础驱动程序已在任务更改卸载功能。

当微型端口驱动程序指示任务卸载更改时，NDIS 将转换为 WMI GUID_NDIS_STATUS_OFFLOAD_CAPABILITIES_CHANGE 事件的 WMI 客户端的状态指示。

包含的数据缓冲区的 NDIS 提供具有 GUID [NDIS_WMI_EVENT_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567900)结构，后跟[NDIS_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff566599)结构。

有关任务卸载功能的详细信息，请参阅[NDIS_STATUS_TASK_OFFLOAD_CURRENT_CONFIG](ndis-status-task-offload-current-config.md)并[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)。

