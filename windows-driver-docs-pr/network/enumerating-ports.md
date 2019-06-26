---
title: 枚举端口
description: 枚举端口
ms.assetid: b38c5556-5124-45ea-af2f-4a4cd9313cc7
keywords:
- 枚举 NDIS 端口 WDK NDIS
- 端口 WDK NDIS OID 请求
- NDIS 端口 WDK，OID 请求
- OID 请求 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77dbf3d94129d784993236f661b26e3dbeb42cd8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354574"
---
# <a name="enumerating-ports"></a>枚举端口





协议的 NDIS 驱动程序和筛选器驱动程序可以使用[OID\_代\_ENUMERATE\_端口](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-enumerate-ports)OID 查询请求以确定活动与相关联的 NDIS 端口的特征基础的微型端口适配器。 NDIS 处理此 OID 和微型端口驱动程序不会收到此 OID 查询。

如果查询成功，NDIS 提供了在查询的结果[ **NDIS\_端口\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_array)结构。 **NumberOfPorts**成员的 NDIS\_端口\_数组包含的活动与微型端口适配器关联的端口号。 **端口**成员的 NDIS\_端口\_数组包含指向的指针的列表[ **NDIS\_端口\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_characteristics)结构。 每个 NDIS\_端口\_特征结构定义的单个端口的特征。

 

 





