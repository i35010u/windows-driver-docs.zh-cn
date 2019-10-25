---
title: GUID_NDIS_STATUS_PACKET_FILTER
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_STATUS_PACKET_FILTER GUID。
ms.assetid: d842862b-5b9f-46bf-aaa9-4542b3a3e047
keywords:
- GUID_NDIS_STATUS_PACKET_FILTER，WDK GUID_NDIS_STATUS_PACKET_FILTER 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa6abc1d219850e0d1ac8d6d9712a1abcac39879
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842387"
---
# <a name="guid_ndis_status_packet_filter"></a>GUID_NDIS_STATUS_PACKET_FILTER

GUID_NDIS_STATUS_PACKET_FILTER 事件 GUID 指示微型端口适配器的数据包筛选器发生了更改。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

NDIS 生成 NDIS_STATUS_PACKET_FILTER 状态指示，通知过量驱动程序，数据包筛选器配置可能发生了更改。

NDIS 将状态指示转换为 WMI 客户端的 WMI GUID_NDIS_STATUS_PACKET_FILTER 事件。

具有 GUID 的 NDIS 提供的数据缓冲区包含后跟 ULONG 值的[NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)结构。 有关数据包筛选器状态和可能值的详细信息，请参阅[OID_GEN_CURRENT_PACKET_FILTER](oid-gen-current-packet-filter.md)。

