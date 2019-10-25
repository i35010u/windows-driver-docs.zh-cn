---
title: GUID_NDIS_STATUS_NETWORK_CHANGE
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_STATUS_NETWORK_CHANGE GUID。
ms.assetid: 4be2b79d-dc99-4096-bf13-54e75deeee56
keywords:
- GUID_NDIS_STATUS_NETWORK_CHANGE，WDK GUID_NDIS_STATUS_NETWORK_CHANGE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: aff2bbbb844dd1ccd5cb39819f8a954954bcc45e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842277"
---
# <a name="guid_ndis_status_network_change"></a>GUID_NDIS_STATUS_NETWORK_CHANGE

GUID_NDIS_STATUS_NETWORK_CHANGE 事件 GUID 指示必须重新协商第三层地址。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

NDIS 或微型端口驱动程序可以生成[NDIS_STATUS_NETWORK_CHANGE](ndis-status-network-change.md)状态指示来报告网络状态的更改。

当微型端口驱动程序或 NDIS 指示网络状态发生更改时，NDIS 会将状态指示转换为 WMI 客户端的 WMI GUID_NDIS_STATUS_NETWORK_CHANGE 事件。

具有此 GUID 的 NDIS 提供的数据缓冲区包含[NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)结构，后跟 NDIS_NETWORK_CHANGE_TYPE 类型的值。 有关可能值的列表，请参阅[NDIS_STATUS_NETWORK_CHANGE](ndis-status-network-change.md)。

