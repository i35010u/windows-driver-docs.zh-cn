---
title: GUID_NDIS_GEN_PORT_STATE
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_GEN_PORT_STATE GUID。
keywords:
- GUID_NDIS_GEN_PORT_STATE，WDK GUID_NDIS_GEN_PORT_STATE 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6eb3a1bc665350fd63fdcf8324e7af47925fca3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799397"
---
# <a name="guid_ndis_gen_port_state"></a>GUID_NDIS_GEN_PORT_STATE

WMI 客户端可以使用 GUID_NDIS_GEN_PORT_STATE 方法 GUID 来获取 NDIS 端口的状态。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

GUID_NDIS_GEN_PORT_STATE 要求使用 WMI 方法请求来返回 NDIS 端口的状态。 应 NDIS_WMI_DEFAULT_METHOD_ID WMI 方法标识符，WMI 输入缓冲区应包含 [NDIS_WMI_METHOD_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header) 的结构。

NDIS 处理此 GUID，微型端口驱动程序不会收到 OID 查询。

NDIS 随 GUID 返回的数据缓冲区包含 [NDIS_PORT_STATE](./oid-gen-port-state.md) 结构。

有关端口状态的详细信息，请参阅 [OID_GEN_PORT_STATE](oid-gen-port-state.md)。
