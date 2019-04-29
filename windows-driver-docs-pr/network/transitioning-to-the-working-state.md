---
title: 转换到工作状态
description: 转换到工作状态
ms.assetid: ad8eb6d7-b542-4208-85f7-fba42c27a9f3
keywords:
- 工作电源状态 WDK 网络
- 网络接口卡 WDK 网络，转换的电源状态
- Nic WDK 网络，转换的电源状态
- 电源管理 WDK NDIS 微型端口转换的电源状态
- 设备电源状态 WDK 网络
- 电源状态 WDK 网络
- 转换电源状态 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e694f0d2987cbef8ad94eda8b0f7693fd7e56e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366137"
---
# <a name="transitioning-to-the-working-state"></a>转换到工作状态





NDIS 发送微型端口驱动程序启动的工作电源状态 (D0) 转换[OID\_PNP\_设置\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)指定状态 D0 的请求。 然后，微型端口驱动程序必须执行还原至工作状态的网络适配器所需的任何依赖于设备的操作。 微型端口驱动程序还必须还原任何硬件上下文，即数据包筛选器、 多播的地址、 当前媒体访问控制 (MAC) 地址或唤醒模式-网络适配器可能已丢失。

**请注意**  支持的微型端口驱动程序从 NDIS 6.30 [NDIS 数据包合并](ndis-packet-coalescing.md)必须清除其合并的数据包计数器。 该驱动程序还必须配置要刷新其合并在低功耗转换之前的任何数据包的网络适配器。 有关详细信息，请参阅[处理数据包合并接收筛选器](handling-packet-coalescing-receive-filters.md)。

 

之前的微型端口驱动程序将返回 NDIS\_状态\_SUCCESS 作为响应到该 OID\_PNP\_设置\_POWER 请求、 微型端口驱动程序和网络适配器必须准备好进行正常操作。

 

 





