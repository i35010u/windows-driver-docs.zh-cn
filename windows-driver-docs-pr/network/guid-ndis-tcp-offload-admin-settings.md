---
title: GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS GUID。
ms.assetid: 8648c75a-dcb3-4723-a2d0-d406d3a073d6
keywords:
- GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS，WDK GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: a88c41b345605a04d8713ba2a58ad0142eae29e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842368"
---
# <a name="guid_ndis_tcp_offload_admin_settings"></a>GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS

WMI 客户端可以使用 GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS set GUID 为 NDIS 端口设置卸载配置参数。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

NDIS 将此 GUID 转换为[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) OID，以设置 NDIS 端口的当前配置。 为任务卸载提供各种支持的 NDIS 微型端口驱动程序必须支持此 OID。

WMI 输入缓冲区包含后跟[NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)结构的[NDIS_WMI_SET_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_set_header)结构。

有关端口参数的详细信息，请参阅[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)。

