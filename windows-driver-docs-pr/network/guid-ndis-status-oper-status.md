---
title: GUID_NDIS_STATUS_OPER_STATUS
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_STATUS_OPER_STATUS GUID。
ms.assetid: e4e13f9d-6298-47b0-9cb1-70fea87db59a
keywords:
- GUID_NDIS_STATUS_OPER_STATUS，WDK GUID_NDIS_STATUS_OPER_STATUS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbaaea0834a5bb2a0e04cf2860f16dc7e2c41aa1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369663"
---
# <a name="guidndisstatusoperstatus"></a>GUID_NDIS_STATUS_OPER_STATUS

GUID_NDIS_STATUS_OPER_STATUS 事件 GUID 表示的 NDIS 网络接口的当前操作状态。 NDIS 6.0 及更高版本支持此 WMI GUID。

生成 NDIS [NDIS_STATUS_OPER_STATUS](ndis-status-oper-status.md)状态指示要报告的 NDIS 网络接口的当前操作状态。

当 NDIS 指示的 NDIS 网络接口的当前操作状态的更改时，NDIS 也将转换为 WMI GUID_NDIS_STATUS_OPER_STATUS 事件的 WMI 客户端的状态指示。

包含的数据缓冲区的 NDIS 提供具有 GUID [NDIS_WMI_EVENT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_event_header)结构，后跟[NDIS_OPER_STATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_oper_state)结构。 有关可能的值的列表，请参阅[NDIS_STATUS_OPER_STATUS](ndis-status-oper-status.md)。

