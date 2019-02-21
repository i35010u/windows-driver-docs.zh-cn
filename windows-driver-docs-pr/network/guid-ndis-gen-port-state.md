---
title: GUID_NDIS_GEN_PORT_STATE
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_GEN_PORT_STATE GUID。
ms.assetid: 0632843e-ea79-4ada-919e-8ab7d94a4421
keywords:
- GUID_NDIS_GEN_PORT_STATE，WDK GUID_NDIS_GEN_PORT_STATE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2909886d1406b833e5926535e4ceeac812ad1a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541080"
---
# <a name="guidndisgenportstate"></a>GUID_NDIS_GEN_PORT_STATE

WMI 客户端可以使用 GUID_NDIS_GEN_PORT_STATE 方法 GUID 获取 NDIS 端口的状态。 NDIS 6.0 及更高版本支持此 WMI GUID。

GUID_NDIS_GEN_PORT_STATE 需要 WMI 方法请求返回的 NDIS 端口的状态。 WMI 方法标识符应 NDIS_WMI_DEFAULT_METHOD_ID，且应包含 WMI 输入的缓冲区[NDIS_WMI_METHOD_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567903)结构。

NDIS 处理此 GUID，并微型端口驱动程序不会收到一个 OID 查询。

NDIS 返回 GUID 的数据缓冲区包含[NDIS_PORT_STATE](https://msdn.microsoft.com/library/windows/hardware/ff569624)结构。

有关端口状态的详细信息，请参阅[OID_GEN_PORT_STATE](oid-gen-port-state.md)。

