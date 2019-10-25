---
title: GUID_NDIS_GEN_LINK_STATE
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_GEN_LINK_STATE GUID。
ms.assetid: 0b0ebb57-33fb-4a18-b6e5-3f4300729280
keywords:
- GUID_NDIS_GEN_LINK_STATE，WDK GUID_NDIS_GEN_LINK_STATE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: af7d1dd054ad9c0468c623a2916bf05a2a43fa02
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842288"
---
# <a name="guid_ndis_gen_link_state"></a>GUID_NDIS_GEN_LINK_STATE

WMI 客户端可以使用 GUID_NDIS_GEN_LINK_STATE 方法 GUID 来确定当前链接状态。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

NDIS 处理此 GUID 和微型端口驱动程序不会收到 OID 查询。

当 WMI 客户端发出 GUID_NDIS_GEN_LINK_STATE WMI 方法请求时，NDIS 返回微型端口适配器或 NDIS 端口的当前链接状态。

WMI 方法标识符应为 NDIS_WMI_DEFAULT_METHOD_ID，WMI 输入缓冲区应包含[NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header)结构。

NDIS 返回的具有此 GUID 的数据缓冲区包含[NDIS_LINK_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构。

微型端口驱动程序在初始化期间提供链接状态，并提供具有状态指示的更新。 当链接状态更改时，WMI 客户端可以使用 GUID_NDIS_GEN_LINK_STATE GUID 接收更新。

有关链接状态的详细信息，请参阅[OID_GEN_LINK_STATE](oid-gen-link-state.md) and [NDIS_STATUS_LINK_STATE](ndis-status-link-state.md)。

