---
title: GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES GUID。
ms.assetid: 5918fcb0-ebcf-4021-99a5-9ecfd2fdb987
keywords:
- GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES，WDK GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55f558b55850ca7b5f1b328a04ee88bb41506d34
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369633"
---
# <a name="guidndistcpoffloadhwcapabilities"></a>GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES

WMI 客户端可以使用 GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES 方法 GUID 来获取与指定的端口的微型端口适配器相关联的硬件支持 TCP 卸载功能。

此 GUID 需要 WMI 方法请求返回的 NDIS 端口的硬件功能。 WMI 方法标识符应 NDIS_WMI_DEFAULT_METHOD_ID，且应包含 WMI 输入的缓冲区[NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_method_header)结构。

NDIS 处理此 GUID，并微型端口驱动程序不会收到一个 OID 查询。

NDIS 返回 GUID 的数据缓冲区包含[NDIS_OFFLOAD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)结构。

有关端口状态的详细信息，请参阅[OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES](oid-tcp-offload-hardware-capabilities.md)。

