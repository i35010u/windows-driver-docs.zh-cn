---
title: 枚举端口
description: 枚举端口
ms.assetid: b38c5556-5124-45ea-af2f-4a4cd9313cc7
keywords:
- 枚举 NDIS 端口 WDK NDIS
- 端口 WDK NDIS，OID 请求
- NDIS 端口 WDK，OID 请求
- OID 请求 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60f261365d9affc54767fca42406eee5d4f726f9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212501"
---
# <a name="enumerating-ports"></a>枚举端口





NDIS 协议驱动程序和筛选器驱动程序可以使用 [oid \_ 代 \_ 枚举 \_ 端口](./oid-gen-enumerate-ports.md) oid 查询请求来确定与基础微型端口适配器关联的活动 NDIS 端口的特征。 NDIS 处理此 OID，微型端口驱动程序不会收到此 OID 查询。

如果查询成功，NDIS 将提供 [**ndis \_ 端口 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_array) 结构中的查询结果。 NDIS **NumberOfPorts**端口数组的 NumberOfPorts \_ 成员 \_ 包含与微型端口适配器关联的活动端口数。 NDIS 端口数组的 **端口** 成员 \_ \_ 包含指向 [**ndis \_ 端口 \_ 特征**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics) 结构的指针的列表。 每个 NDIS \_ 端口 \_ 特征结构定义单个端口的特征。

 

