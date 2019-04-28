---
title: GUID_NDIS_STATUS_PORT_STATE
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_STATUS_PORT_STATE GUID。
ms.assetid: c657eef6-eb80-4715-9d60-0d2dde403300
keywords:
- GUID_NDIS_STATUS_PORT_STATE，WDK GUID_NDIS_STATUS_PORT_STATE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cd62de203e732d306abd348d1b67e535fc0c87d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349854"
---
# <a name="guidndisstatusportstate"></a>GUID_NDIS_STATUS_PORT_STATE

GUID_NDIS_STATUS_PORT_STATE 事件 GUID 表示的 NDIS 端口状态的更改。 NDIS 6.0 及更高版本支持此 WMI GUID。

支持 NDIS 端口使用的微型端口驱动程序[NDIS_STATUS_PORT_STATE](ndis-status-port-state.md)状态指示，指示在 NDIS 端口的状态更改。

当微型端口驱动程序指示端口状态更改时，NDIS 将转换为 WMI GUID_NDIS_STATUS_PORT_STATE 事件的 WMI 客户端的状态指示。

NDIS 提供具有此 GUID 的数据缓冲区包含[NDIS_WMI_EVENT_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567900)结构，后跟[NDIS_PORT_STATE](https://msdn.microsoft.com/library/windows/hardware/ff569624)结构。

有关端口状态的详细信息，请参阅[OID_GEN_PORT_STATE](oid-gen-port-state.md)。

