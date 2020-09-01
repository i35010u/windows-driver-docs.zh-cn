---
title: GUID_NDIS_GEN_PORT_STATE
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_GEN_PORT_STATE GUID。
ms.assetid: 0632843e-ea79-4ada-919e-8ab7d94a4421
keywords:
- GUID_NDIS_GEN_PORT_STATE，WDK GUID_NDIS_GEN_PORT_STATE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8851ac5161ff52a663cb79e8530f01a72e988abf
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207557"
---
# <a name="guid_ndis_gen_port_state"></a>GUID_NDIS_GEN_PORT_STATE

WMI 客户端可以使用 GUID_NDIS_GEN_PORT_STATE 方法 GUID 来获取 NDIS 端口的状态。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

GUID_NDIS_GEN_PORT_STATE 要求使用 WMI 方法请求来返回 NDIS 端口的状态。 应 NDIS_WMI_DEFAULT_METHOD_ID WMI 方法标识符，WMI 输入缓冲区应包含 [NDIS_WMI_METHOD_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header) 的结构。

NDIS 处理此 GUID，微型端口驱动程序不会收到 OID 查询。

NDIS 随 GUID 返回的数据缓冲区包含 [NDIS_PORT_STATE](./oid-gen-port-state.md) 结构。

有关端口状态的详细信息，请参阅 [OID_GEN_PORT_STATE](oid-gen-port-state.md)。