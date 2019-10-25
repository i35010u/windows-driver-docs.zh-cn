---
title: GUID_NDIS_STATUS_PORT_STATE
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_STATUS_PORT_STATE GUID。
ms.assetid: c657eef6-eb80-4715-9d60-0d2dde403300
keywords:
- GUID_NDIS_STATUS_PORT_STATE，WDK GUID_NDIS_STATUS_PORT_STATE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: c314ac9e32e9285af553cdfde32ea8ab7985d3d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842371"
---
# <a name="guid_ndis_status_port_state"></a>GUID_NDIS_STATUS_PORT_STATE

GUID_NDIS_STATUS_PORT_STATE 事件 GUID 指示 NDIS 端口状态的更改。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

支持 NDIS 端口的微型端口驱动程序使用[NDIS_STATUS_PORT_STATE](ndis-status-port-state.md)状态指示来指示 NDIS 端口状态的更改。

当微型端口驱动程序指示端口状态更改时，NDIS 会将状态指示转换为 WMI 客户端的 WMI GUID_NDIS_STATUS_PORT_STATE 事件。

NDIS 使用此 GUID 提供的数据缓冲区包含后跟[NDIS_PORT_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state)结构的[NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)结构。

有关端口状态的详细信息，请参阅[OID_GEN_PORT_STATE](oid-gen-port-state.md)。

