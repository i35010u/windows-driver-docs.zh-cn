---
title: SD 卡驱动程序堆栈
description: SD 卡驱动程序堆栈
ms.assetid: 196739bb-530f-4a60-98a0-ece0b4c5ef34
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
ms.openlocfilehash: 437f76be200944e7677987dbe216d7d1f9299554
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824731"
---
# <a name="sd-card-driver-stack"></a>SD 卡驱动程序堆栈


安全数字（SD）卡技术从可移植的小型内存卡开始，但在安全数字 i/o （SDIO）规范的发行版中，安全数字协会（SDA）已扩大了 SD 技术的定义，以包含大量纸牌功能，如 Bluetooth 设备、摄像机、无线 LAN 设备和全球定位系统（GPS）接收器。 本文档介绍操作系统如何支持将卡函数扩展到 SD 技术。

许多早期 SD 存储设备的卡读取器旨在连接到 USB 总线。 Windows 将通过 USB 大容量存储驱动程序（*usbstor*）和本机存储类驱动程序（*sys.databases*）来管理这些设备，如下图所示：

![说明早期 sd 存储设备的设备堆栈的关系图](images/sdio-usb.png)

有关 Windows 为连接到 USB 总线的内存卡创建的设备堆栈的更完整说明，请参阅[USB 大容量存储设备的设备对象示例](https://docs.microsoft.com/windows-hardware/drivers/storage/device-object-example-for-a-usb-mass-storage-device)。

操作系统支持直接连接到 PCI 总线的 SD 主机控制器。 当系统枚举 SD 主机控制器时，它会加载本机 SD 总线驱动程序（*sdbus*）。 如果用户插入 SD 内存卡，Windows 将在总线驱动程序的顶层加载本机 SD 存储类驱动程序（*sffdisk*）和存储微型端口驱动程序（*sffp\_* 。 如果用户插入具有其他类型功能的 SD 卡（例如 GPS 或无线 LAN），则 Windows 会加载供应商为该设备提供的驱动程序。

SD 堆栈中的所有设备驱动程序，无论是本机还是供应商提供的，都必须通过调用静态 SD bus 库（*sdbus*）中的例程与 sd bus 驱动程序通信。 SD 驱动程序必须在编译时链接到此库。 下图描述了系统在枚举 SD 控制器和随附卡时创建的 SD 驱动程序堆栈：

![说明 sd 软件和硬件组件之间的关系的关系图](images/sdiostack.png)

SD 设备驱动程序不能直接访问主机控制器注册集，也不能在 i/o 请求数据包（Irp）中为主机控制器嵌入传递命令。 SD 设备驱动程序通过调用 SD bus 库例程向主机控制器发出命令，然后库为主机控制器生成相应的 SD 命令。

SD 设备驱动程序必须处理标准 PnP 和电源 Irp，但不会请求或管理硬件资源，如端口、内存或中断矢量。 因此，在处理[**IRP\_MN\_START\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求时，不需要使用 SD 设备驱动程序来映射任何硬件资源。 但是，当 SD 设备驱动程序收到[**IRP\_MN\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)请求时，它必须停止所有 i/o 操作。 而且，驱动程序必须关闭其到 SD bus 驱动程序的接口，才能响应[**IRP\_MN\_QUERY\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)请求。

发生硬件中断时，SD 总线库会截获中断，屏蔽进一步的中断，并通过发生硬件中断的回调例程通知 SD 设备驱动程序。 有关总线驱动程序用于向 SD 设备驱动程序通知硬件中断的回调例程的说明，请参阅[**PSDBUS\_回调\_例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nc-ntddsd-sdbus_callback_routine)。 有关 SD 驱动程序堆栈和库如何管理硬件中断的一般说明，请参阅[处理安全数字（SD）硬件中断](https://docs.microsoft.com/windows-hardware/drivers/sd/handling-sd-card-interrupts)。

Windows 驱动程序工具包（WDK）中提供的*ntddsd*头文件声明 SD bus 库公开的例程的原型。

 

 




