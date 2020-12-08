---
title: GUID_NDIS_TCP_OFFLOAD_CAPABILITIES
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_TCP_OFFLOAD_CAPABILITIES GUID。
keywords:
- GUID_NDIS_TCP_OFFLOAD_CAPABILITIES，WDK GUID_NDIS_TCP_OFFLOAD_CAPABILITIES 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71f3ec33413403f8aa5a4776c784dfffcde9d38a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836783"
---
# <a name="guid_ndis_tcp_offload_capabilities"></a>GUID_NDIS_TCP_OFFLOAD_CAPABILITIES

WMI 客户端可以使用 GUID_NDIS_TCP_OFFLOAD_CAPABILITIES 方法 GUID 来获取与微型端口适配器的指定端口关联的任务卸载功能。

此 GUID 需要 WMI 方法请求才能返回 NDIS 端口的卸载功能。 应 NDIS_WMI_DEFAULT_METHOD_ID WMI 方法标识符，WMI 输入缓冲区应包含 [NDIS_WMI_METHOD_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header) 的结构。

NDIS 处理此 GUID，微型端口驱动程序不会收到 OID 查询。

NDIS 随 GUID 返回的数据缓冲区包含 [NDIS_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload) 结构。

有关端口状态的详细信息，请参阅 [OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)。
