---
title: GUID_NDIS_ENUMERATE_ADAPTERS_EX
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_ENUMERATE_ADAPTERS_EX GUID。
ms.assetid: 46c4c127-a9f6-4555-82d1-3c537fbb7914
keywords:
- GUID_NDIS_ENUMERATE_ADAPTERS_EX，WDK GUID_NDIS_ENUMERATE_ADAPTERS_EX 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 573deb221fb2faa1a3b5ece05946834a04d04393
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207573"
---
# <a name="guid_ndis_enumerate_adapters_ex"></a>GUID_NDIS_ENUMERATE_ADAPTERS_EX

WMI 客户端可以使用 GUID_NDIS_ENUMERATE_ADAPTERS_EX GUID 获取计算机上所有微型端口适配器的枚举。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。 由于 NDIS 跟踪所有加载的微型端口适配器，因此 NDIS 不会查询微型端口驱动程序以获取此信息。

WMI 客户端可以使用此 GUID 在[NDIS_WMI_ENUM_ADAPTER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_enum_adapter)结构的**NetLuid**成员中查找设备名称和关联值。 WMI 客户端可以在后续的 GUID 请求中使用适配器的 **NetLuid** 值。

NDIS 返回的具有 GUID 的数据缓冲区包含 NDIS_WMI_ENUM_ADAPTER 结构的数组。