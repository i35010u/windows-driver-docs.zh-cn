---
title: GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES GUID。
ms.assetid: 5918fcb0-ebcf-4021-99a5-9ecfd2fdb987
keywords:
- GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES，WDK GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18d16cb442881ebe9a7d28a6a9f4fc5992a81def
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842364"
---
# <a name="guid_ndis_tcp_offload_hw_capabilities"></a>GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES

WMI 客户端可以使用 GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES 方法 GUID 来获取与微型端口适配器的指定端口关联的硬件支持的 TCP 卸载功能。

此 GUID 需要一个 WMI 方法请求来返回 NDIS 端口的硬件功能。 WMI 方法标识符应为 NDIS_WMI_DEFAULT_METHOD_ID，WMI 输入缓冲区应包含[NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header)结构。

NDIS 处理此 GUID，微型端口驱动程序不会收到 OID 查询。

NDIS 随 GUID 返回的数据缓冲区包含[NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构。

有关端口状态的详细信息，请参阅[OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES](oid-tcp-offload-hardware-capabilities.md)。

