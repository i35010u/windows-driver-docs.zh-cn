---
title: GUID_NDIS_ENUMERATE_ADAPTERS_EX
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_ENUMERATE_ADAPTERS_EX GUID。
keywords:
- GUID_NDIS_ENUMERATE_ADAPTERS_EX，WDK GUID_NDIS_ENUMERATE_ADAPTERS_EX 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfcbcd0d322c79196e89f2a55fe018fcbc7d08c3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816599"
---
# <a name="guid_ndis_enumerate_adapters_ex"></a>GUID_NDIS_ENUMERATE_ADAPTERS_EX

WMI 客户端可以使用 GUID_NDIS_ENUMERATE_ADAPTERS_EX GUID 获取计算机上所有微型端口适配器的枚举。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。 由于 NDIS 跟踪所有加载的微型端口适配器，因此 NDIS 不会查询微型端口驱动程序以获取此信息。

WMI 客户端可以使用此 GUID 在 [NDIS_WMI_ENUM_ADAPTER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_enum_adapter)结构的 **NetLuid** 成员中查找设备名称和关联值。 WMI 客户端可以在后续的 GUID 请求中使用适配器的 **NetLuid** 值。

NDIS 返回的具有 GUID 的数据缓冲区包含 NDIS_WMI_ENUM_ADAPTER 结构的数组。
