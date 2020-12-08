---
title: 已注册到 WMI 的标准微型端口驱动程序 OID
description: 已注册到 WMI 的标准微型端口驱动程序 OID
keywords:
- 小型端口适配器 WDK 网络，WMI
- 适配器 WDK 网络，WMI
- WMI WDK 网络，Oid
- Oid WDK 网络，WMI
- Windows Management Instrumentation WDK 网络，Oid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bbe6096d03a0223c8f105ae03e821f801da68dd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795865"
---
# <a name="standard-miniport-driver-oids-registered-with-wmi"></a>已注册到 WMI 的标准微型端口驱动程序 OID





NDIS 为微型端口适配器将 WMI Guid 注册到 WMI。 为了获取微型端口适配器支持的 Oid 列表，NDIS 向关联的微型端口驱动程序发出 [oid 生成 \_ 支持的 \_ \_ 列表](./oid-gen-supported-list.md) 查询。 微型端口驱动程序必须提供微型端口适配器支持的所有 Oid 的列表。 此列表必须包含所有必需的 Oid，并且应包含可选的和自定义 Oid （如果有）。

NDIS 将支持的 Oid 映射到 WMI Guid，并将 Guid 注册到 WMI。 如果需要，NDIS 会将 WMI GUID 请求转换为已注册 Oid 的 OID 请求。

NDIS 驱动程序还可以将自定义 Guid 注册到 WMI。 有关自定义 Guid 的详细信息，请参阅 [自定义 oid 和状态指示](customized-oids-and-status-indications.md)。

NDIS 还会将状态指示转换为 WMI 事件。 有关将状态指示转换为 WMI 事件的详细信息，请参阅 [在 wmi 中注册的标准微型端口驱动程序状态](standard-miniport-driver-status-indications-registered-with-wmi.md)。

 

