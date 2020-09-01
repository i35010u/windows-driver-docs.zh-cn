---
title: 已注册到 WMI 的标准微型端口驱动程序 OID
description: 已注册到 WMI 的标准微型端口驱动程序 OID
ms.assetid: 87529f7f-8d62-4067-b008-7c4a04d7a7c6
keywords:
- 小型端口适配器 WDK 网络，WMI
- 适配器 WDK 网络，WMI
- WMI WDK 网络，Oid
- Oid WDK 网络，WMI
- Windows Management Instrumentation WDK 网络，Oid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42b2a1d39b804fddbb1ad796bac899811d792c20
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216556"
---
# <a name="standard-miniport-driver-oids-registered-with-wmi"></a>已注册到 WMI 的标准微型端口驱动程序 OID





NDIS 为微型端口适配器将 WMI Guid 注册到 WMI。 为了获取微型端口适配器支持的 Oid 列表，NDIS 向关联的微型端口驱动程序发出 [oid 生成 \_ 支持的 \_ \_ 列表](./oid-gen-supported-list.md) 查询。 微型端口驱动程序必须提供微型端口适配器支持的所有 Oid 的列表。 此列表必须包含所有必需的 Oid，并且应包含可选的和自定义 Oid （如果有）。

NDIS 将支持的 Oid 映射到 WMI Guid，并将 Guid 注册到 WMI。 如果需要，NDIS 会将 WMI GUID 请求转换为已注册 Oid 的 OID 请求。

NDIS 驱动程序还可以将自定义 Guid 注册到 WMI。 有关自定义 Guid 的详细信息，请参阅 [自定义 oid 和状态指示](customized-oids-and-status-indications.md)。

NDIS 还会将状态指示转换为 WMI 事件。 有关将状态指示转换为 WMI 事件的详细信息，请参阅 [在 wmi 中注册的标准微型端口驱动程序状态](standard-miniport-driver-status-indications-registered-with-wmi.md)。

 

