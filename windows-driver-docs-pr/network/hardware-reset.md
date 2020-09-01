---
title: 微型端口驱动程序硬件重置
description: 微型端口驱动程序硬件重置
ms.assetid: d5209809-039c-4ac2-afdf-1f5144307850
keywords:
- 网络接口卡 WDK 网络，重置
- Nic WDK 网络，重置
- 重置 NIC
- MiniportResetEx
- 硬件重置 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50085472137d2ab5fb5390bb53d6a18a9fe5e2fa
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214752"
---
# <a name="miniport-driver-hardware-reset"></a>微型端口驱动程序硬件重置





微型端口驱动程序必须向[**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)注册[*MiniportResetEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)函数。

*MiniportResetEx* 可以通过调用 [**NdisMResetComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete) (同步或异步完成，请参阅下图) 。

![阐释重置网络接口卡的示意图](images/207-09.png)

*MiniportResetEx* 应：

-   禁用进一步中断。

-   清除与任何正在进行的发送相关联的数据。 例如，在总线主机直接内存访问 (DMA) 设备的环形缓冲区上，应清除发送缓冲区的指针。 反序列化和面向连接的微型端口驱动程序必须 \_ \_ \_ 为任何排队发送请求中止 NDIS 状态请求。

-   将硬件状态和微型端口驱动程序的内部状态还原到重置操作之前已存在的状态。

微型端口驱动程序负责还原设备的硬件状态（多播地址、数据包筛选器、任务卸载设置和唤醒模式除外）。 这些设置由微型端口驱动程序或 NDIS 还原。 微型端口驱动程序通过在 *AddressingReset* 参数中返回一个布尔值，来确定负责还原这些设置的人员。

如果微型端口驱动程序在*AddressingReset*参数中返回**FALSE** ，微型端口驱动程序会将其多播地址、数据包筛选器、任务卸载设置和唤醒模式还原到初始状态。 如果微型端口驱动程序在*AddressingReset*中返回**TRUE** ，NDIS 将调用无连接微型端口驱动程序的[*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数或面向连接的微型端口驱动程序的[**MiniportCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)函数来设置以下配置设置：

-   通过 [OID 生成 \_ \_ 当前 \_ 数据包 \_ 筛选器](./oid-gen-current-packet-filter.md)的集请求来进行网络数据包筛选。

-   通过 [OID \_ 802 \_ 3 \_ 多播 \_ 列表](./oid-802-3-multicast-list.md)的设置请求的多路广播地址列表。

-   任务卸载通过 [OID \_ 卸载 \_ 封装](./oid-offload-encapsulation.md)的 set 请求来封装设置。

-   电源管理唤醒模式通过 [OID \_ PNP \_ 添加 \_ 唤醒 \_ \_ 模式](./oid-pnp-add-wake-up-pattern.md)的设置请求。
    **注意**   从 NDIS 6.20 开始，通过 OID PM 设置的唤醒[模式 \_ \_ 添加 \_ WOL \_ 模式](./oid-pm-add-wol-pattern.md)必须通过微型端口驱动程序还原。

     

## <a name="related-topics"></a>相关主题


[微型端口驱动程序的适配器状态](adapter-states-of-a-miniport-driver.md)

[微型端口适配器状态和操作](miniport-adapter-states-and-operations.md)

[微型端口驱动程序重置和停止函数](/previous-versions/windows/hardware/network/ff564064(v=vs.85))

 

