---
title: 微型端口驱动程序硬件重置
description: 微型端口驱动程序硬件重置
ms.assetid: d5209809-039c-4ac2-afdf-1f5144307850
keywords:
- 网络接口卡 WDK 网络、 重置
- Nic WDK 网络、 重置
- 重置 NIC
- MiniportResetEx
- 硬件重置 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 910ddf81b74e9e316d4de863609c0f1e91390d25
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342628"
---
# <a name="miniport-driver-hardware-reset"></a>微型端口驱动程序硬件重置





微型端口驱动程序必须注册[ *MiniportResetEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559432)函数与[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)。

*MiniportResetEx*可以通过调用完成同步或异步[ **NdisMResetComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563663)（请参阅下图）。

![说明重置网络接口卡的关系图](images/207-09.png)

*MiniportResetEx*应：

-   禁用进一步中断。

-   清除与任何关联的数据将发送正在进行中。 例如，在总线 master 直接内存访问 (DMA) 设备的环形缓冲区，应清除发送缓冲区的指针。 反序列化和面向连接的微型端口驱动程序必须返回 NDIS\_状态\_请求\_排队的发送的任何请求被中止。

-   硬件状态和微型端口驱动程序的内部状态还原到重置操作之前已存在的状态。

微型端口驱动程序负责将除多播的地址、 数据包筛选器、 任务卸载设置和模式唤醒设备硬件状态还原。 这些设置将还原由微型端口驱动程序或 NDIS。 微型端口驱动程序确定由谁来负责通过返回一个布尔值中的将这些设置还原*AddressingReset*参数。

如果微型端口驱动程序将返回**FALSE**中*AddressingReset*参数，微型端口驱动程序将还原其多播的地址，数据包筛选器、 任务卸载设置和唤醒模式相对于其初始状态。 如果微型端口驱动程序将返回 **，则返回 TRUE**中*AddressingReset*，NDIS 调用无连接的微型端口驱动程序[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)函数或面向连接的微型端口驱动程序的[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)函数可设置以下配置设置：

-   通过设置请求的网络数据包筛选器[OID\_代\_当前\_数据包\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569575)。

-   通过设置请求的多播的地址列表[OID\_802\_3\_多播\_列表](https://msdn.microsoft.com/library/windows/hardware/ff569073)。

-   任务卸载封装设置的 set 请求通过[OID\_卸载\_封装](https://msdn.microsoft.com/library/windows/hardware/ff569762)。

-   电源管理唤醒模式通过的集请求[OID\_PNP\_添加\_唤醒\_向上\_模式](https://msdn.microsoft.com/library/windows/hardware/ff569773)。
    **请注意**  从 NDIS 6.20 开始，通过设置唤醒模式[OID\_PM\_添加\_WOL\_模式](https://msdn.microsoft.com/library/windows/hardware/ff569764)微型端口驱动程序必须还原。

     

## <a name="related-topics"></a>相关主题


[适配器状态的微型端口驱动程序](adapter-states-of-a-miniport-driver.md)

[微型端口适配器状态和操作](miniport-adapter-states-and-operations.md)

[微型端口驱动程序重置和 Halt 函数](https://msdn.microsoft.com/library/windows/hardware/ff564064)

 

 






