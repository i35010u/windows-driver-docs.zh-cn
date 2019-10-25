---
title: GUID_NDIS_STATUS_OPER_STATUS
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_STATUS_OPER_STATUS GUID。
ms.assetid: e4e13f9d-6298-47b0-9cb1-70fea87db59a
keywords:
- GUID_NDIS_STATUS_OPER_STATUS，WDK GUID_NDIS_STATUS_OPER_STATUS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: b081821c516cd345c75bcfa97affad4490528c90
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842375"
---
# <a name="guid_ndis_status_oper_status"></a>GUID_NDIS_STATUS_OPER_STATUS

GUID_NDIS_STATUS_OPER_STATUS 事件 GUID 指示 NDIS 网络接口的当前操作状态。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

NDIS 生成[NDIS_STATUS_OPER_STATUS](ndis-status-oper-status.md)状态指示来报告 NDIS 网络接口的当前操作状态。

当 NDIS 指示 NDIS 网络接口的当前操作状态发生更改时，NDIS 还会将状态指示转换为 WMI 客户端的 WMI GUID_NDIS_STATUS_OPER_STATUS 事件。

具有 GUID 的 NDIS 提供的数据缓冲区包含后跟[NDIS_OPER_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_oper_state)结构的[NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_event_header)结构。 有关可能值的列表，请参阅[NDIS_STATUS_OPER_STATUS](ndis-status-oper-status.md)。

