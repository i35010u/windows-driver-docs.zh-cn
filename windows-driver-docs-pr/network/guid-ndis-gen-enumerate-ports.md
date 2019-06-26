---
title: GUID_NDIS_GEN_ENUMERATE_PORTS
description: 本主题介绍 NDIS WMI 接口的 GUID_NDIS_GEN_ENUMERATE_PORTS GUID。
ms.assetid: c7572ff2-c9e1-4605-9768-b14636ce007f
keywords:
- GUID_NDIS_GEN_ENUMERATE_PORTS，WDK GUID_NDIS_GEN_ENUMERATE_PORTS 网络驱动程序
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a2fddf9920673bb462b025d8d3f1c234d17568b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382741"
---
# <a name="guidndisgenenumerateports"></a>GUID_NDIS_GEN_ENUMERATE_PORTS

WMI 客户端可以使用 GUID_NDIS_GEN_ENUMERATE_PORTS 方法 GUID 来获取与微型端口适配器关联的端口的列表。 NDIS 6.0 及更高版本支持此 WMI GUID。

NDIS 处理此请求，并微型端口驱动程序不会收到一个 OID 查询。

GUID_NDIS_GEN_ENUMERATE_PORTS 需要 WMI 方法请求枚举端口。 WMI 方法标识符应为 NDIS_WMI_DEFAULT_METHOD_ID。 应包含 WMI 输入的缓冲区[NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_method_header)结构，它标识中的微型端口适配器的 NDIS 网络接口名称**NetLuid**成员并指定为零**PortNumber**成员。 WMI 客户端可以获取**NetLuid**值的适配器[GUID_NDIS_ENUMERATE_ADAPTERS_EX](guid-ndis-enumerate-adapters-ex.md)方法 GUID。

NDIS 返回 GUID 的数据缓冲区包含[NDIS_PORT_ARRAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_array)结构。 **NumberOfPorts** NDIS_PORT_ARRAY 成员包含与微型端口适配器相关联的活动端口数。 **端口**NDIS_PORT_ARRAY 成员包含指向的指针的列表[NDIS_PORT_CHARACTERISTICS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_characteristics)结构。 每个 NDIS_PORT_CHARACTERISTICS 结构定义单个 NDIS 端口的特征。

枚举端口的详细信息，请参阅[OID_GEN_ENUMERATE_PORTS](oid-gen-enumerate-ports.md)。

