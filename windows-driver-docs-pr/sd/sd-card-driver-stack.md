---
title: SD 卡驱动程序堆栈
description: SD 卡驱动程序堆栈
ms.assetid: 196739bb-530f-4a60-98a0-ece0b4c5ef34
keywords:
- SD WDK 总线，驱动程序堆栈
- 驱动程序堆栈 WDK SD 总线
- 堆栈 WDK SD 总线
- 设备堆栈 WDK SD 总线
- SDIO WDK 总线
- 安全数字 I/O WDK 总线
- 主机控制器 WDK SD 总线
- 硬件 WDK SD 总线
- 软件 WDK SD 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e4a041bbfe09be7f489c8a1e938fd1e2c800466
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325962"
---
# <a name="sd-card-driver-stack"></a>SD 卡驱动程序堆栈


安全数字 (SD) 卡技术开始采用可移植，小型内存卡，但安全数字 I/O (SDIO) 规范的版本中，安全数字关联 (SDA) 已扩大了的 SD 技术，以包括大量不同的定义卡函数，如 Bluetooth 的设备、 摄像机、 无线 LAN 的设备，以及全球定位系统 (GPS) 接收器。 本文档介绍如何在操作系统支持 SD 技术的卡函数扩展。

很多早期 SD 存储设备的卡读卡器不仅可以连接到 USB 总线。 Windows 管理这些设备使用 USB 大容量存储驱动程序 (*usbstor.sys*) 和本机存储类驱动程序 (*disk.sys*) 下, 图中所示：

![说明一个早期 sd 存储设备的设备堆栈的关系图](images/sdio-usb.png)

Windows 会为连接到 USB 总线的内存卡创建设备堆栈的更完整说明，请参阅[USB 大容量存储设备的设备对象示例](https://msdn.microsoft.com/library/windows/hardware/ff552547)。

操作系统支持直接连接到 PCI 总线的 SD 主机控制器。 时系统枚举 SD 主控制器时，它会加载本机 SD 总线驱动程序 (*sdbus.sys*)。 如果用户插入 SD 内存卡，Windows 将加载本机 SD 存储类驱动程序 (*sffdisk.sys*) 和存储微型端口驱动程序 (*sffp\_sd.sys*) 在总线驱动程序之上。 如果用户插入具有其他类型功能的 SD 卡（例如 GPS 或无线 LAN），则 Windows 会加载供应商为该设备提供的驱动程序。

SD 堆栈中的所有设备驱动程序是否本机或供应商提供，必须与都通信 SD 总线驱动程序通过调用静态 SD 总线库中的例程 (*sdbus.lib*)。 在编译时，SD 驱动程序必须链接到此库。 下图描绘了它枚举 SD 控制器以及随附的卡时，系统会创建 SD 驱动程序堆栈：

![说明 sd 软件和硬件组件之间的关系的关系图](images/sdiostack.png)

SD 设备驱动程序不能直接访问主控制器注册组，也可以在主控制器传递命令中嵌入 I/O 请求数据包 (Irp)。 SD 设备驱动程序通过调用 SD 总线库例程，向主控制器发出命令，然后在库生成主控制器的适当 SD 命令。

SD 设备驱动程序必须处理标准的即插即用和电源 Irp，但不是执行操作请求或管理硬件资源，例如端口、 内存、 或中断向量。 因此，SD 设备驱动程序不需要映射的任何硬件资源时处理[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)请求。 但是，当 SD 设备驱动程序收到[ **IRP\_MN\_停止\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551755)请求，它必须停止所有 I/O 操作。 此外，驱动程序必须关闭到 SD 总线驱动程序以响应其界面[ **IRP\_MN\_查询\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551705)请求。

硬件中断发生时，SD 总线库截获中断、 遮盖进一步中断，并通过的硬件中断发生的回调例程通知 SD 设备驱动程序。 回调例程总线驱动程序用于通知的硬件中断的 SD 设备驱动程序的说明，请参阅[ **PSDBUS\_回调\_例程**](https://msdn.microsoft.com/library/windows/hardware/ff537617)。 SD 驱动程序堆栈和库如何管理硬件中断的常规说明，请参阅[处理 Secure Digital (SD) 硬件中断](https://msdn.microsoft.com/library/windows/hardware/ff537177)。

*Ntddsd.h*头文件，它提供 Windows Driver Kit (WDK) 中，声明由 SD 总线库公开的例程的原型。

 

 




