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
ms.openlocfilehash: 4a838a33bcd8c338541b90db37d1ff713cb4caa6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842549"
---
# <a name="miniport-driver-hardware-reset"></a>微型端口驱动程序硬件重置





微型端口驱动程序必须向[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)注册[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)函数。

*MiniportResetEx*可以通过调用[**NdisMResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete)同步或异步完成（见下图）。

![阐释重置网络接口卡的示意图](images/207-09.png)

*MiniportResetEx*应：

-   禁用进一步中断。

-   清除与任何正在进行的发送相关联的数据。 例如，在总线主机直接内存访问（DMA）设备的环形缓冲区上，应清除发送缓冲区的指针。 反序列化和面向连接的微型端口驱动程序必须返回 NDIS\_状态\_请求在任何排队发送请求\_中止。

-   将硬件状态和微型端口驱动程序的内部状态还原到重置操作之前已存在的状态。

微型端口驱动程序负责还原设备的硬件状态（多播地址、数据包筛选器、任务卸载设置和唤醒模式除外）。 这些设置由微型端口驱动程序或 NDIS 还原。 微型端口驱动程序通过在*AddressingReset*参数中返回一个布尔值，来确定负责还原这些设置的人员。

如果微型端口驱动程序在*AddressingReset*参数中返回**FALSE** ，微型端口驱动程序会将其多播地址、数据包筛选器、任务卸载设置和唤醒模式还原到初始状态。 如果微型端口驱动程序在*AddressingReset*中返回**TRUE** ，NDIS 将调用无连接微型端口驱动程序的[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数或面向连接的微型端口驱动程序的[**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)函数来设置以下配置设置：

-   通过 OID 的 set 请求来进行网络数据包筛选[\_代\_当前\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)。

-   通过[OID\_802\_3\_多播\_列表](https://docs.microsoft.com/windows-hardware/drivers/network/oid-802-3-multicast-list)的设置请求的多路广播地址列表。

-   任务卸载通过[OID\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)设置来封装设置。

-   电源管理唤醒模式：通过将[OID\_PNP\_添加\_唤醒\_向上\_模式](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-add-wake-up-pattern)。
    **请注意**  从 NDIS 6.20 开始，通过 OID 设置的唤醒模式[\_PM\_添加\_WOL\_模式](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-wol-pattern)必须通过微型端口驱动程序还原。

     

## <a name="related-topics"></a>相关主题


[微型端口驱动程序的适配器状态](adapter-states-of-a-miniport-driver.md)

[微型端口适配器状态和操作](miniport-adapter-states-and-operations.md)

[微型端口驱动程序重置和暂停函数](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff564064(v=vs.85))

 

 






