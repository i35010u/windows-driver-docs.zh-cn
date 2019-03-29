---
title: GUID_NDIS_STATUS_PACKET_FILTER
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_STATUS_PACKET_FILTER GUID。
ms.assetid: d842862b-5b9f-46bf-aaa9-4542b3a3e047
keywords:
- GUID_NDIS_STATUS_PACKET_FILTER，WDK GUID_NDIS_STATUS_PACKET_FILTER 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54984c805ac7a4fd6e6825df6406d75d967b3cfc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567579"
---
# <a name="guidndisstatuspacketfilter"></a>GUID_NDIS_STATUS_PACKET_FILTER

GUID_NDIS_STATUS_PACKET_FILTER 事件 GUID 表示已被微型端口适配器的数据包筛选器中的更改。 NDIS 6.0 及更高版本支持此 WMI GUID。

NDIS 生成 NDIS_STATUS_PACKET_FILTER 状态指示通知基础驱动程序，可能有数据包筛选器配置中的更改。

NDIS 将转换到 WMI GUID_NDIS_STATUS_PACKET_FILTER 事件的 WMI 客户端的状态指示。

包含的数据缓冲区的 NDIS 提供具有 GUID [NDIS_WMI_EVENT_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567900)后跟 ULONG 值的结构。 有关数据包筛选器状态和可能的值的详细信息，请参阅[OID_GEN_CURRENT_PACKET_FILTER](oid-gen-current-packet-filter.md)。

