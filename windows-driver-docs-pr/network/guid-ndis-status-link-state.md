---
title: GUID_NDIS_STATUS_LINK_STATE
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_STATUS_LINK_STATE GUID。
ms.assetid: 7f56d211-14c7-4b8b-8d1c-ee7836b7b70a
keywords:
- GUID_NDIS_STATUS_LINK_STATE，WDK GUID_NDIS_STATUS_LINK_STATE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5240daac815b7b1bc255465fd6f11c22b39b1256
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521496"
---
# <a name="guidndisstatuslinkstate"></a>GUID_NDIS_STATUS_LINK_STATE

GUID_NDIS_STATUS_LINK_STATE 事件 GUID 表示已处于链接状态的微型端口适配器的更改。 NDIS 6.0 及更高版本支持此 WMI GUID。

微型端口驱动程序使用[NDIS_STATUS_LINK_STATE](ndis-status-link-state.md)状态指示通知 NDIS 和基础驱动程序已处于链接状态更改。

当微型端口驱动程序指示链接状态更改时，NDIS 将转换为 WMI GUID_NDIS_STATUS_LINK_STATE 事件的 WMI 客户端的状态指示。

包含的数据缓冲区的 NDIS 提供具有 GUID [NDIS_WMI_EVENT_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567900)结构，后跟[NDIS_LINK_STATE](https://msdn.microsoft.com/library/windows/hardware/hh205390)结构。 **NDIS_LINK_STATE**结构指定的介质的物理状态。

有关链接状态的详细信息，请参阅[OID_GEN_LINK_STATE](oid-gen-link-state.md)并[NDIS_STATUS_LINK_STATE](ndis-status-link-state.md)。

