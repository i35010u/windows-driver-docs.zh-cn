---
title: GUID_NDIS_STATUS_NETWORK_CHANGE
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_STATUS_NETWORK_CHANGE GUID。
keywords:
- GUID_NDIS_STATUS_NETWORK_CHANGE，WDK GUID_NDIS_STATUS_NETWORK_CHANGE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fc5490af9757fbebc15f7e235bf0b9178c1f6db
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838749"
---
# <a name="guid_ndis_status_network_change"></a>GUID_NDIS_STATUS_NETWORK_CHANGE

GUID_NDIS_STATUS_NETWORK_CHANGE 事件 GUID 指示必须重新协商第三层地址。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

NDIS 或微型端口驱动程序可以生成 [NDIS_STATUS_NETWORK_CHANGE](ndis-status-network-change.md) 状态指示来报告网络状态的更改。

当微型端口驱动程序或 NDIS 指示网络状态发生更改时，NDIS 会将状态指示转换为 WMI 客户端的 WMI GUID_NDIS_STATUS_NETWORK_CHANGE 事件。

NDIS 通过此 GUID 提供的数据缓冲区包含后跟 NDIS_NETWORK_CHANGE_TYPE 类型值的 [NDIS_WMI_EVENT_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header) 结构。 有关可能值的列表，请参阅 [NDIS_STATUS_NETWORK_CHANGE](ndis-status-network-change.md)。
