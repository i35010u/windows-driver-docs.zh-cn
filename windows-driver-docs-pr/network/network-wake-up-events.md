---
title: 网络唤醒事件
description: 网络唤醒事件
ms.assetid: 85195d44-4d79-4feb-af35-c478dc4319c5
keywords:
- 唤醒功能 WDK 网络类型
- Nic WDK 网络连接、 唤醒事件
- 网络接口卡 WDK 网络连接、 唤醒事件
- Magic 数据包 WDK 网络
- 有关唤醒功能唤醒功能 WDK 网络
- 网络唤醒事件 WDK 网络
- 电源管理 WDK NDIS 微型端口，唤醒功能
- 唤醒帧 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 835f99f4b4af8465f37ff43bfcdb9238b0585c52
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542906"
---
# <a name="network-wake-up-events"></a>网络唤醒事件





一个*网络唤醒事件*是导致唤醒系统的网络适配器的外部事件。 网络适配器通过断言最终会导致系统从睡眠状态到工作状态进行转换的特定于总线的唤醒信号唤醒系统。

NDIS 定义以下两个网络唤醒事件：

-   包含指定的绑定的协议驱动程序的模式的网络唤醒帧的回执。

-   幻数据包的回执。

网络适配器可以支持网络唤醒事件，包括无根本的任意组合。 NDIS 处理时微型端口驱动程序设置来处理微型端口驱动程序，因为不电源管理感知**布尔**的成员[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)到**NULL**。

具体取决于网络适配器的功能，可以从任何设备电源状态，包括 highest-powered 状态 (D0) 发生网络唤醒事件。

### <a name="network-wake-up-frames"></a>网络唤醒帧

如果在初始化期间，微型端口驱动程序指示网络适配器可以发出信号的数据包，包含指定的模式接收唤醒，绑定的协议可以启用基于模式的唤醒网络适配器上的方法，并指定唤醒模式。 若要启用这种类型的唤醒，协议驱动程序设置 NDIS\_PNP\_唤醒\_向上\_模式\_中的匹配项标志[OID\_PNP\_启用\_唤醒\_向上](https://msdn.microsoft.com/library/windows/hardware/ff569775)。

协议驱动程序将使用[OID\_PNP\_添加\_唤醒\_向上\_模式](https://msdn.microsoft.com/library/windows/hardware/ff569773)来指定唤醒模式，以及一个屏蔽，它指示传入数据包的字节数应使用模式进行比较。 协议驱动程序可以删除唤醒模式与[OID\_PNP\_删除\_唤醒\_向上\_模式](https://msdn.microsoft.com/library/windows/hardware/ff569779)。

有关网络唤醒帧的详细信息，请参阅[网络设备的电源管理](https://go.microsoft.com/fwlink/p/?linkid=9945)。

### <a name="magic-packet-wake-up"></a>幻数据包唤醒

一个*幻数据包*是包含 16 个连续副本接收的网络适配器的 MAC 地址的数据包。

本部分包括：

[启用唤醒事件](enabling-wake-up-events.md)

[处理唤醒事件](handling-wake-up-events.md)

 

 





