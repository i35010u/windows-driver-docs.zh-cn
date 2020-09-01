---
title: GUID_NDIS_TCP_OFFLOAD_CAPABILITIES
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_TCP_OFFLOAD_CAPABILITIES GUID。
ms.assetid: 93b8af60-3c15-4eea-a0ea-ce1c71f0b60c
keywords:
- GUID_NDIS_TCP_OFFLOAD_CAPABILITIES，WDK GUID_NDIS_TCP_OFFLOAD_CAPABILITIES 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c8451f49d315e1d8cd84342ef973d94b6822b3e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217628"
---
# <a name="guid_ndis_tcp_offload_capabilities"></a>GUID_NDIS_TCP_OFFLOAD_CAPABILITIES

WMI 客户端可以使用 GUID_NDIS_TCP_OFFLOAD_CAPABILITIES 方法 GUID 来获取与微型端口适配器的指定端口关联的任务卸载功能。

此 GUID 需要 WMI 方法请求才能返回 NDIS 端口的卸载功能。 应 NDIS_WMI_DEFAULT_METHOD_ID WMI 方法标识符，WMI 输入缓冲区应包含 [NDIS_WMI_METHOD_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header) 的结构。

NDIS 处理此 GUID，微型端口驱动程序不会收到 OID 查询。

NDIS 随 GUID 返回的数据缓冲区包含 [NDIS_OFFLOAD](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload) 结构。

有关端口状态的详细信息，请参阅 [OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)。