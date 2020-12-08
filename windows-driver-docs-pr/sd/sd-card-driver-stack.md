---
title: SD 卡驱动程序堆栈
description: SD 卡驱动程序堆栈
keywords:
- SD WDK 总线，驱动程序堆栈
- 驱动程序堆栈 WDK SD 总线
- 堆积 WDK SD 总线
- 设备堆栈 WDK SD 总线
- SDIO WDK 总线
- 保护数字 i/o WDK 总线
- 主机控制器 WDK SD bus
- 硬件 WDK SD 总线
- 软件 WDK SD 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbf6643e2117b5a3d52afd16f68a62dd8677ca3c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831125"
---
# <a name="sd-card-driver-stack"></a>SD 卡驱动程序堆栈


安全数字 (SD) 卡技术从可移植的小型内存卡开始，但随着安全数字 i/o (SDIO) 规范的发布，安全数字协会 (SDA) 已扩大了了 SD 技术的定义，以包含大量卡功能，如 Bluetooth 设备、视频相机、无线 LAN 设备和全球定位系统 (GPS) 接收器。 本文档介绍操作系统如何支持将卡函数扩展到 SD 技术。

许多早期 SD 存储设备的卡读取器旨在连接到 USB 总线。 Windows 将通过 USB 大容量存储驱动程序 (*usbstor.sys*) 和本机存储类驱动程序 (*disk.sys*) 来管理这些设备，如下图所示：

![说明早期 sd 存储设备的设备堆栈的关系图](images/sdio-usb.png)

有关 Windows 为连接到 USB 总线的内存卡创建的设备堆栈的更完整说明，请参阅 [USB 大容量存储设备的设备对象示例](../storage/device-object-example-for-a-usb-mass-storage-device.md)。

操作系统支持直接连接到 PCI 总线的 SD 主机控制器。 当系统枚举 SD 主机控制器时，它将 (*sdbus.sys*) 加载本机 SD 总线驱动程序。 如果用户插入 SD 内存卡，Windows 将在总线驱动程序的顶层 (*sffdisk.sys*) 和存储微型端口驱动程序 (*sffp \_sd.sys*) 加载本机 SD 存储类驱动程序。 如果用户插入具有其他类型功能的 SD 卡（例如 GPS 或无线 LAN），则 Windows 会加载供应商为该设备提供的驱动程序。

SD 堆栈中的所有设备驱动程序，无论是本机还是供应商提供的，都必须通过调用静态 SD bus 库 (*sdbus*) 中的例程来与 sd 总线驱动程序通信。 SD 驱动程序必须在编译时链接到此库。 下图描述了系统在枚举 SD 控制器和随附卡时创建的 SD 驱动程序堆栈：

![说明 sd 软件和硬件组件之间的关系的关系图](images/sdiostack.png)

SD 设备驱动程序不能直接访问主机控制器注册集，也不能在 (Irp) 的 i/o 请求数据包中为主机控制器嵌入传递命令。 SD 设备驱动程序通过调用 SD bus 库例程向主机控制器发出命令，然后库为主机控制器生成相应的 SD 命令。

SD 设备驱动程序必须处理标准 PnP 和电源 Irp，但不会请求或管理硬件资源，如端口、内存或中断矢量。 因此，在处理 [**IRP \_ MN \_ 开始 \_ 设备**](../kernel/irp-mn-start-device.md) 请求时，SD 设备驱动程序无需映射任何硬件资源。 但是，当 SD 设备驱动程序收到 [**IRP \_ MN \_ 停止 \_ 设备**](../kernel/irp-mn-stop-device.md) 请求时，它必须停止所有 i/o 操作。 而且，驱动程序必须关闭其到 SD bus 驱动程序的接口，才能响应 [**IRP \_ MN \_ 查询 \_ 删除 \_ 设备**](../kernel/irp-mn-query-remove-device.md) 请求。

发生硬件中断时，SD 总线库会截获中断，屏蔽进一步的中断，并通过发生硬件中断的回调例程通知 SD 设备驱动程序。 有关总线驱动程序用于向 SD 设备驱动程序通知硬件中断的回调例程的说明，请参阅 [**PSDBUS \_ 回调 \_ 例程**](/windows-hardware/drivers/ddi/ntddsd/nc-ntddsd-sdbus_callback_routine)。 有关 SD 驱动程序堆栈和库如何管理硬件中断的一般说明，请参阅 [处理安全数字 (SD) 硬件中断](./handling-sd-card-interrupts.md)。

Windows 驱动程序工具包 (WDK) 中提供的 *ntddsd* 标头文件声明 SD 总线库公开的例程的原型。

 

