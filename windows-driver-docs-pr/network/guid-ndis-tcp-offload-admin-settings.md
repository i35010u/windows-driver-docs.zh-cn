---
title: GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS GUID。
keywords:
- GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS，WDK GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: da740c60a0f0ba26bb7e5340c8aa8351d3667984
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836785"
---
# <a name="guid_ndis_tcp_offload_admin_settings"></a>GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS

WMI 客户端可以使用 GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS 集 GUID 为 NDIS 端口设置卸载配置参数。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

NDIS 将此 GUID 转换为 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) OID，以设置 NDIS 端口的当前配置。 为任务卸载提供各种支持的 NDIS 微型端口驱动程序必须支持此 OID。

WMI 输入缓冲区包含后跟[NDIS_OFFLOAD_PARAMETERS](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)结构的[NDIS_WMI_SET_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_set_header)结构。

有关端口参数的详细信息，请参阅 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)。
