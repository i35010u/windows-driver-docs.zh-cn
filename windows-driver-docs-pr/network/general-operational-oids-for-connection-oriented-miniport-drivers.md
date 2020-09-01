---
title: 面向连接的微型端口驱动程序的常规操作 OID
description: 本主题介绍面向连接的对象的常规操作 Oid。
ms.assetid: 38a8a256-b70e-4ba9-bc95-f1a2965493b2
keywords:
- 面向操作 Oid 连接的常规小型小型驱动程序
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6390a2ba4afcbffdf9db902b8f0268b74d9c5b5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207601"
---
# <a name="general-operational-oids-for-connection-oriented-miniport-drivers"></a>面向连接的微型端口驱动程序的常规操作 OID

下表总结了用于获取或设置面向连接的微型端口驱动程序和/或其 Nic 的一般操作特征的 Oid。

> [!TIP] 
> 面向连接的微型端口驱动程序在其 [MiniportCoOidRequest](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request) 回调函数中处理此类请求。

在此表中，M 指示 OID 是必需的，而 O 指示它是可选的。

| Length | 查询 | 设置 | 名称 |
| --- | --- | --- | --- |
| 2 | M |   | [OID_GEN_CO_DRIVER_VERSION](oid-gen-co-driver-version.md) |
| 8 | O |   | [OID_GEN_CO_GET_NETCARD_TIME](oid-gen-co-get-netcard-time.md) |
| 8 | O |   | [OID_GEN_CO_GET_TIME_CAPS](oid-gen-co-get-time-caps.md) |
| 4 | M |   | [OID_GEN_CO_HARDWARE_STATUS](oid-gen-co-hardware-status.md) |
| 4 | M |   | [OID_GEN_CO_LINK_SPEED](oid-gen-co-link-speed.md) |
| 4 | M |   | [OID_GEN_CO_MAC_OPTIONS](oid-gen-co-mac-options.md) |
| 4 | M |   | [OID_GEN_CO_MEDIA_CONNECT_STATUS](oid-gen-co-media-connect-status.md) |
| Arr (4)  | M |   | [OID_GEN_CO_MEDIA_IN_USE](oid-gen-co-media-in-use.md) |
| Arr (4)  | M |   | [OID_GEN_CO_MEDIA_SUPPORTED](oid-gen-co-media-supported.md) |
| 4 | M |   | [OID_GEN_CO_MINIMUM_LINK_SPEED](oid-gen-co-minimum-link-speed.md) |
| 4 |   | M | [OID_GEN_CO_PROTOCOL_OPTIONS](oid-gen-co-protocol-options.md) |
| Arr | O |   | [OID_GEN_CO_SUPPORTED_GUIDS](oid-gen-co-supported-guids.md) |
| Arr (4)  | M |   | [OID_GEN_CO_SUPPORTED_LIST](oid-gen-co-supported-list.md) |
| 差. | M |   | [OID_GEN_CO_VENDOR_DESCRIPTION](oid-gen-co-vendor-description.md) |
| 4 | M |   | [OID_GEN_CO_VENDOR_DRIVER_VERSION](oid-gen-co-vendor-driver-version.md) |
| 4 | M |   | [OID_GEN_CO_VENDOR_ID](oid-gen-co-vendor-id.md) |