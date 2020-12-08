---
title: GUID_NDIS_STATUS_OPER_STATUS
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_STATUS_OPER_STATUS GUID。
keywords:
- GUID_NDIS_STATUS_OPER_STATUS，WDK GUID_NDIS_STATUS_OPER_STATUS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53775a0079293d074f7d658d8530a516a6103ae9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836791"
---
# <a name="guid_ndis_status_oper_status"></a>GUID_NDIS_STATUS_OPER_STATUS

GUID_NDIS_STATUS_OPER_STATUS 事件 GUID 指示 NDIS 网络接口的当前操作状态。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

NDIS 生成 [NDIS_STATUS_OPER_STATUS](ndis-status-oper-status.md) 状态指示来报告 NDIS 网络接口的当前操作状态。

当 NDIS 指示 NDIS 网络接口的当前操作状态发生更改时，NDIS 还会将状态指示转换为 WMI 客户端的 WMI GUID_NDIS_STATUS_OPER_STATUS 事件。

具有 GUID 的 NDIS 提供的数据缓冲区包含后跟[NDIS_OPER_STATE](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_oper_state)结构的[NDIS_WMI_EVENT_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)结构。 有关可能值的列表，请参阅 [NDIS_STATUS_OPER_STATUS](ndis-status-oper-status.md)。
