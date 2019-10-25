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
ms.openlocfilehash: 95cb831fe209a4b3c6e2979afc57daa7cdc355db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834770"
---
# <a name="enumerating-ports"></a>枚举端口





NDIS 协议驱动程序和筛选器驱动程序可以使用[OID\_代\_枚举\_端口](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-enumerate-ports)OID 查询请求，以确定与基础微型端口适配器关联的活动 NDIS 端口的特征。 NDIS 处理此 OID，微型端口驱动程序不会收到此 OID 查询。

如果查询成功，NDIS\_端口提供查询的结果[ **\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_array)结构。 NDIS\_端口\_阵列的**NumberOfPorts**成员包含与微型端口适配器关联的活动端口数。 NDIS\_端口\_数组的**端口**成员包含指向[**NDIS\_端口\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)结构的指针的列表。 每个 NDIS\_端口\_特征结构定义单个端口的特征。

 

 





