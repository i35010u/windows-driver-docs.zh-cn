---
title: 转换到工作状态
description: 转换到工作状态
ms.assetid: ad8eb6d7-b542-4208-85f7-fba42c27a9f3
keywords:
- 工作电源状态 WDK 网络
- 网络接口卡 WDK 网络，过渡电源状态
- Nic WDK 网络，过渡电源状态
- 电源管理 WDK NDIS 微型端口，转换电源状态
- 设备电源状态 WDK 网络
- 电源状态 WDK 网络
- 转换电源状态 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 118266c6f488eb807bc8554a0f10000e21c5fa20
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215807"
---
# <a name="transitioning-to-the-working-state"></a>转换到工作状态





NDIS 通过向指定状态 D0 的 [OID \_ PNP \_ 集 \_ 电源](./oid-pnp-set-power.md) 请求发送微型端口驱动程序，启动到工作电源状态的转换 (D0) 。 然后，微型端口驱动程序必须执行将网络适配器还原到正常工作状态所需的任何设备相关操作。 微型端口驱动程序还必须还原任何硬件上下文-数据包筛选器、多播地址、当前的媒体访问控制 (MAC) 地址或唤醒模式--网络适配器可能已丢失。

**注意**   从 NDIS 6.30 开始，支持[NDIS 数据包合并](ndis-packet-coalescing.md)的微型端口驱动程序必须清除其合并的数据包计数器。 驱动程序还必须将网络适配器配置为刷新在低功耗转换之前合并的任何数据包。 有关详细信息，请参阅 [处理包合并接收筛选器](handling-packet-coalescing-receive-filters.md)。

 

在小型端口驱动程序返回 NDIS \_ 状态 \_ "成功" 以响应 OID \_ PNP \_ 设置 \_ 电源请求之前，微型端口驱动程序和网络适配器必须已准备就绪，可以正常操作。

 

