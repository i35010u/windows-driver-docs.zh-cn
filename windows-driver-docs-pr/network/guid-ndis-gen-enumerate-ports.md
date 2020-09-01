---
title: GUID_NDIS_GEN_ENUMERATE_PORTS
description: 本主题描述了 NDIS WMI 接口的 GUID_NDIS_GEN_ENUMERATE_PORTS GUID。
ms.assetid: c7572ff2-c9e1-4605-9768-b14636ce007f
keywords:
- GUID_NDIS_GEN_ENUMERATE_PORTS，WDK GUID_NDIS_GEN_ENUMERATE_PORTS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: bec5e3814daf65ff01fb02ea3bcdca3a5d69dc99
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207569"
---
# <a name="guid_ndis_gen_enumerate_ports"></a>GUID_NDIS_GEN_ENUMERATE_PORTS

WMI 客户端可以使用 GUID_NDIS_GEN_ENUMERATE_PORTS 方法 GUID 来获取与微型端口适配器关联的端口列表。 在 NDIS 6.0 和更高版本中支持此 WMI GUID。

NDIS 处理此请求，微型端口驱动程序不会收到 OID 查询。

GUID_NDIS_GEN_ENUMERATE_PORTS 要求使用 WMI 方法请求来枚举端口。 WMI 方法标识符应 NDIS_WMI_DEFAULT_METHOD_ID。 WMI 输入缓冲区应包含一个 [NDIS_WMI_METHOD_HEADER](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header) 结构，该结构标识 **NetLuid** 成员中的微型端口适配器的 NDIS 网络接口名称，并为 **PortNumber** 成员指定零。 WMI 客户端可以获取具有[GUID_NDIS_ENUMERATE_ADAPTERS_EX](guid-ndis-enumerate-adapters-ex.md)方法 GUID 的适配器的**NetLuid**值。

NDIS 随 GUID 返回的数据缓冲区包含 [NDIS_PORT_ARRAY](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_array) 结构。 NDIS_PORT_ARRAY 的 **NumberOfPorts** 成员包含与微型端口适配器关联的活动端口数。 NDIS_PORT_ARRAY 的 **端口** 成员包含指向 [NDIS_PORT_CHARACTERISTICS](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics) 结构的指针的列表。 每个 NDIS_PORT_CHARACTERISTICS 结构都定义了单个 NDIS 端口的特征。

有关枚举端口的详细信息，请参阅 [OID_GEN_ENUMERATE_PORTS](oid-gen-enumerate-ports.md)。