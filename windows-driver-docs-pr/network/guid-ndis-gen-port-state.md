---
title: GUID_NDIS_GEN_PORT_STATE
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_GEN_PORT_STATE GUID。
ms.assetid: 0632843e-ea79-4ada-919e-8ab7d94a4421
keywords:
- GUID_NDIS_GEN_PORT_STATE，WDK GUID_NDIS_GEN_PORT_STATE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c7c7b3f98eadbe8ed0002fe41a543fd4f250324
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382701"
---
# <a name="guidndisgenportstate"></a>GUID_NDIS_GEN_PORT_STATE

WMI 客户端可以使用 GUID_NDIS_GEN_PORT_STATE 方法 GUID 获取 NDIS 端口的状态。 NDIS 6.0 及更高版本支持此 WMI GUID。

GUID_NDIS_GEN_PORT_STATE 需要 WMI 方法请求返回的 NDIS 端口的状态。 WMI 方法标识符应 NDIS_WMI_DEFAULT_METHOD_ID，且应包含 WMI 输入的缓冲区[NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_method_header)结构。

NDIS 处理此 GUID，并微型端口驱动程序不会收到一个 OID 查询。

NDIS 返回 GUID 的数据缓冲区包含[NDIS_PORT_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-state)结构。

有关端口状态的详细信息，请参阅[OID_GEN_PORT_STATE](oid-gen-port-state.md)。

