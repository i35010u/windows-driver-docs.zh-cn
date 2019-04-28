---
title: GUID_NDIS_STATUS_OPER_STATUS
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_STATUS_OPER_STATUS GUID。
ms.assetid: e4e13f9d-6298-47b0-9cb1-70fea87db59a
keywords:
- GUID_NDIS_STATUS_OPER_STATUS，WDK GUID_NDIS_STATUS_OPER_STATUS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63232d47b9f373c1588f748effb87e236071b68c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349834"
---
# <a name="guidndisstatusoperstatus"></a>GUID_NDIS_STATUS_OPER_STATUS

GUID_NDIS_STATUS_OPER_STATUS 事件 GUID 表示的 NDIS 网络接口的当前操作状态。 NDIS 6.0 及更高版本支持此 WMI GUID。

生成 NDIS [NDIS_STATUS_OPER_STATUS](ndis-status-oper-status.md)状态指示要报告的 NDIS 网络接口的当前操作状态。

当 NDIS 指示的 NDIS 网络接口的当前操作状态的更改时，NDIS 也将转换为 WMI GUID_NDIS_STATUS_OPER_STATUS 事件的 WMI 客户端的状态指示。

包含的数据缓冲区的 NDIS 提供具有 GUID [NDIS_WMI_EVENT_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567900)结构，后跟[NDIS_OPER_STATE](https://msdn.microsoft.com/library/windows/hardware/ff566737)结构。 有关可能的值的列表，请参阅[NDIS_STATUS_OPER_STATUS](ndis-status-oper-status.md)。

