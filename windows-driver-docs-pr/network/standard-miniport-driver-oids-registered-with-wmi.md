---
title: 已注册到 WMI 的标准微型端口驱动程序 OID
description: 已注册到 WMI 的标准微型端口驱动程序 OID
ms.assetid: 87529f7f-8d62-4067-b008-7c4a04d7a7c6
keywords:
- 微型端口适配器 WDK 网络 WMI
- 适配器 WDK 网络 WMI
- WMI WDK 网络、 Oid
- Oid WDK 网络 WMI
- Windows Management Instrumentation WDK 网络 Oid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c14ba331e67b3833fa1608ffd56b5e5b2c4bbb71
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353290"
---
# <a name="standard-miniport-driver-oids-registered-with-wmi"></a>已注册到 WMI 的标准微型端口驱动程序 OID





NDIS 注册到 WMI Guid WMI 的微型端口适配器。 若要获取的 Oid 的微型端口适配器支持，NDIS 问题列表[OID\_代\_支持\_列表](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-list)到关联的微型端口驱动程序的查询。 微型端口驱动程序必须提供所有微型端口适配器支持的 Oid 的列表。 此列表必须包含所有必需的 Oid，如果有的话，应包含可选的自定义 Oid。

NDIS 映射到 WMI Guid 的受支持的 Oid 并注册 WMI Guid。 NDIS 转换 WMI GUID 请求 OID 请求，如有必要，为已注册的 Oid。

NDIS 驱动程序还可以向 WMI 注册自定义 Guid。 有关自定义 Guid 的详细信息，请参阅[自定义 Oid 和状态指示](customized-oids-and-status-indications.md)。

NDIS 也意味着，对 WMI 事件的状态指示。 考虑将其转换状态指示 WMI 事件的详细信息，请参阅[标准微型端口驱动程序状态已注册与 WMI](standard-miniport-driver-status-indications-registered-with-wmi.md)。

 

 





