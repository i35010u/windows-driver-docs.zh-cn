---
title: GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS GUID。
ms.assetid: 8648c75a-dcb3-4723-a2d0-d406d3a073d6
keywords:
- GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS，WDK GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 702cc30eb8ba56c7b82406205f262e758839e59b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369654"
---
# <a name="guidndistcpoffloadadminsettings"></a>GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS

WMI 客户端可以使用 GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS 集 GUID 以设置 NDIS 端口的配置参数的卸载。 NDIS 6.0 及更高版本支持此 WMI GUID。

NDIS 转换到此 GUID [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) OID NDIS 端口的当前配置设置。 提供任务卸载的任何类型的支持的 NDIS 微型端口驱动程序必须支持此 OID。

WMI 输入的缓冲区包含[NDIS_WMI_SET_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_set_header)结构，后跟[NDIS_OFFLOAD_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload_parameters)结构。

端口参数的详细信息，请参阅[OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)。

