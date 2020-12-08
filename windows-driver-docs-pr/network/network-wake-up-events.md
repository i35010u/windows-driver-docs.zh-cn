---
title: 关于网络唤醒事件
description: 关于网络唤醒事件
keywords:
- 唤醒功能，WDK 网络，类型
- Nic WDK 网络，唤醒事件
- 网络接口卡 WDK 网络，唤醒事件
- 幻数据包 WDK 网络
- 有关唤醒功能的唤醒功能，WDK 网络
- 网络唤醒事件 WDK 网络
- 电源管理 WDK NDIS 微型端口，唤醒功能
- 唤醒帧 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8840652e72bc7bf9e6f5e4557720b17ad09b9d95
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787214"
---
# <a name="about-network-wake-up-events"></a>关于网络唤醒事件





*网络唤醒事件* 是导致网络适配器唤醒系统的外部事件。 网络适配器通过断言特定于总线的唤醒信号唤醒系统，最终会导致系统从睡眠状态转换到工作状态。

NDIS 定义以下两个网络唤醒事件：

-   接收包含由绑定协议驱动程序指定的模式的网络唤醒帧。

-   接收幻数据包。

网络适配器可支持网络唤醒事件的任意组合，包括全部无。 如果微型端口驱动程序将 [**ndis \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)的 **PowerManagementCapabilities** 成员设置为 **NULL**，ndis 会将微型端口驱动程序视为不支持电源管理。

根据网络适配器的功能，可能会出现网络唤醒事件，其中包括最高的设备电源状态 (D0) 。

### <a name="network-wake-up-frames"></a>网络 Wake-Up 帧

如果在初始化期间，微型端口驱动程序指示网络适配器可以在接收包含指定模式的数据包时发出唤醒信号，则绑定协议可以在网络适配器上启用基于模式的唤醒方法，并指定唤醒模式。 若要启用这种类型的唤醒，协议驱动程序会 \_ \_ \_ \_ \_ 在 [OID \_ pnp \_ enable \_ 唤醒 \_ ](./oid-pnp-enable-wake-up.md)中设置 NDIS pnp 唤醒模式匹配标志。

协议驱动程序使用 [OID \_ PNP \_ 添加 \_ 唤醒 \_ \_ 模式](./oid-pnp-add-wake-up-pattern.md) 来指定唤醒模式，以及指示应将传入数据包的哪些字节与模式进行比较的掩码。 协议驱动程序可以删除具有 [OID \_ PNP \_ 删除 \_ 唤醒 \_ \_ 模式](./oid-pnp-remove-wake-up-pattern.md)的唤醒模式。

有关网络唤醒帧的详细信息，请参阅 [网络设备的电源管理](https://go.microsoft.com/fwlink/p/?linkid=9945)。

### <a name="magic-packet-wake-up"></a>Magic-Packet Wake-Up

*幻数据包* 是包含接收网络适配器的 MAC 地址的16个连续副本的数据包。

本节包括：

[启用唤醒事件](enabling-wake-up-events.md)

[处理唤醒事件](handling-wake-up-events.md)

 

