---
title: GUID_NDIS_ENUMERATE_ADAPTERS_EX
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_ENUMERATE_ADAPTERS_EX GUID。
ms.assetid: 46c4c127-a9f6-4555-82d1-3c537fbb7914
keywords:
- GUID_NDIS_ENUMERATE_ADAPTERS_EX，WDK GUID_NDIS_ENUMERATE_ADAPTERS_EX 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e9f9ca45bfda7fa968277f62a4c8d9961a613f8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842177"
---
# <a name="guid_ndis_enumerate_adapters_ex"></a>GUID_NDIS_ENUMERATE_ADAPTERS_EX

WMI 客户端可以使用 GUID_NDIS_ENUMERATE_ADAPTERS_EX GUID 获取计算机上所有微型端口适配器的枚举。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。 由于 NDIS 跟踪所有加载的微型端口适配器，因此 NDIS 不会查询微型端口驱动程序以获取此信息。

WMI 客户端可以使用此 GUID 在[NDIS_WMI_ENUM_ADAPTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_enum_adapter)结构的**NetLuid**成员中查找设备名称和关联的值。 WMI 客户端可以在后续的 GUID 请求中使用适配器的**NetLuid**值。

NDIS 返回且 GUID 包含 NDIS_WMI_ENUM_ADAPTER 结构数组的数据缓冲区。

