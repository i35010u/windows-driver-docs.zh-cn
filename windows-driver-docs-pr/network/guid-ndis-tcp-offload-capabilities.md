---
title: GUID_NDIS_TCP_OFFLOAD_CAPABILITIES
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_TCP_OFFLOAD_CAPABILITIES GUID。
ms.assetid: 93b8af60-3c15-4eea-a0ea-ce1c71f0b60c
keywords:
- GUID_NDIS_TCP_OFFLOAD_CAPABILITIES，WDK GUID_NDIS_TCP_OFFLOAD_CAPABILITIES 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86208084d85be1f9be2e89b4ab44b794a0d3a7cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355121"
---
# <a name="guidndistcpoffloadcapabilities"></a>GUID_NDIS_TCP_OFFLOAD_CAPABILITIES

WMI 客户端可以使用 GUID_NDIS_TCP_OFFLOAD_CAPABILITIES 方法 GUID 来获取与指定的端口的微型端口适配器相关联的卸载功能的任务。

此 GUID 需要 WMI 方法请求返回的 NDIS 端口的卸载功能。 WMI 方法标识符应 NDIS_WMI_DEFAULT_METHOD_ID，且应包含 WMI 输入的缓冲区[NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_method_header)结构。

NDIS 处理此 GUID，并微型端口驱动程序不会收到一个 OID 查询。

NDIS 返回 GUID 的数据缓冲区包含[NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构。

有关端口状态的详细信息，请参阅[OID_TCP_OFFLOAD_CURRENT_CONFIG](oid-tcp-offload-current-config.md)。

