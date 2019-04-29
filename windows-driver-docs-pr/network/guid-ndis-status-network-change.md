---
title: GUID_NDIS_STATUS_NETWORK_CHANGE
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_STATUS_NETWORK_CHANGE GUID。
ms.assetid: 4be2b79d-dc99-4096-bf13-54e75deeee56
keywords:
- GUID_NDIS_STATUS_NETWORK_CHANGE，WDK GUID_NDIS_STATUS_NETWORK_CHANGE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05501d68bedf1ffbb3e366187154345adb3d51d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361069"
---
# <a name="guidndisstatusnetworkchange"></a>GUID_NDIS_STATUS_NETWORK_CHANGE

GUID_NDIS_STATUS_NETWORK_CHANGE 事件 GUID 表示的三层地址必须重新协商。 NDIS 6.0 及更高版本支持此 WMI GUID。

NDIS 或微型端口驱动程序才能生成[NDIS_STATUS_NETWORK_CHANGE](ndis-status-network-change.md)状态指示报告网络状态中的更改。

当微型端口驱动程序或 NDIS 指示网络状态中的更改时，NDIS 将转换为 WMI GUID_NDIS_STATUS_NETWORK_CHANGE 事件的 WMI 客户端的状态指示。

NDIS 提供具有此 GUID 的数据缓冲区包含[NDIS_WMI_EVENT_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567900)跟 NDIS_NETWORK_CHANGE_TYPE 类型化值的结构。 有关可能的值的列表，请参阅[NDIS_STATUS_NETWORK_CHANGE](ndis-status-network-change.md)。

