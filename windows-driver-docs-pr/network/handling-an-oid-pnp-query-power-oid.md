---
title: 处理 OID_PNP_QUERY_POWER OID
description: 处理 OID_PNP_QUERY_POWER OID
ms.assetid: aec9393a-debb-41eb-a8a0-b3d1936d707b
keywords:
- OID_PNP_QUERY_POWER
- 网络接口卡 WDK 网络，过渡电源状态
- Nic WDK 网络，过渡电源状态
- 电源管理 WDK NDIS 微型端口，转换电源状态
- 设备电源状态 WDK 网络
- 电源状态 WDK 网络
- 转换电源状态 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2d5995c5ca4c458634bc04e6fa08ce01a05b561
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218416"
---
# <a name="handling-an-oid_pnp_query_power-oid"></a>处理 OID \_ PNP \_ 查询 \_ 电源 OID





[Oid \_ PNP \_ 查询 \_ 电源](./oid-pnp-query-power.md)oid 请求微型端口驱动程序，以指示是否可以将网络适配器转换为低功耗状态。 小型端口驱动程序必须始终返回 NDIS \_ 状态 \_ "成功" 以响应 OID \_ PNP 查询电源的查询 \_ \_ 。 通过将 NDIS \_ 状态 \_ 成功返回到此 OID 请求，微型端口驱动程序可保证在收到后续 [OID \_ PNP \_ 设置 \_ 电源](./oid-pnp-set-power.md) 请求时，它会将网络适配器转换为指定的设备电源状态。 在这种情况下，微型端口驱动程序必须不执行任何操作来危害转换。

[Oid \_ pnp \_ 查询 \_ 电源](./oid-pnp-query-power.md)请求始终后跟 oid \_ pnp \_ 设置 \_ 电源请求。 [Oid pnp \_ \_ 集 \_ 电源](./oid-pnp-set-power.md)请求可以紧跟在 oid pnp 查询 \_ 电源请求之后， \_ \_ 或以指定的间隔到达 oid \_ pnp \_ 查询 \_ 电源请求之后。 如果设备状态为 D0，它是在 OID \_ pnp 设置电源请求中指定的，则会 \_ \_ 有效地取消前面的 OID \_ pnp \_ 查询 \_ 电源请求。

 

