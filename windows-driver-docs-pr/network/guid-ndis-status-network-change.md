---
title: GUID_NDIS_STATUS_NETWORK_CHANGE
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_STATUS_NETWORK_CHANGE GUID。
ms.assetid: 4be2b79d-dc99-4096-bf13-54e75deeee56
keywords:
- GUID_NDIS_STATUS_NETWORK_CHANGE，WDK GUID_NDIS_STATUS_NETWORK_CHANGE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3edc23b36ace906631263d246b5dc531a3ee9ab0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218101"
---
# <a name="guid_ndis_status_network_change"></a>GUID_NDIS_STATUS_NETWORK_CHANGE

GUID_NDIS_STATUS_NETWORK_CHANGE 事件 GUID 指示必须重新协商第三层地址。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

NDIS 或微型端口驱动程序可以生成 [NDIS_STATUS_NETWORK_CHANGE](ndis-status-network-change.md) 状态指示来报告网络状态的更改。

当微型端口驱动程序或 NDIS 指示网络状态发生更改时，NDIS 会将状态指示转换为 WMI 客户端的 WMI GUID_NDIS_STATUS_NETWORK_CHANGE 事件。

NDIS 通过此 GUID 提供的数据缓冲区包含后跟 NDIS_NETWORK_CHANGE_TYPE 类型值的 [NDIS_WMI_EVENT_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header) 结构。 有关可能值的列表，请参阅 [NDIS_STATUS_NETWORK_CHANGE](ndis-status-network-change.md)。