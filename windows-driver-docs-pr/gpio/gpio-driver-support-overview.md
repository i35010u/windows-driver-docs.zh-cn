---
title: GPIO 驱动程序支持概述
description: 从 Windows 8，GPIO 框架扩展开始 (GpioClx) 简化了编写 GPIO 控制器设备的驱动程序的任务。
ms.assetid: 450E7F80-D9AC-4F52-8062-2DA5343C8D0F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdd49c365f797b1271206f9af87ecdde0a16b686
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521266"
---
# <a name="gpio-driver-support-overview"></a>GPIO 驱动程序支持概述


从 Windows 8，GPIO 框架扩展开始 (GpioClx) 简化了编写 GPIO 控制器设备的驱动程序的任务。 此外，GpioClx 为连接到 GPIO 插针的外围设备提供驱动程序支持。 GpioClx，是对内核模式驱动程序框架 (KMDF) 系统提供的扩展，执行处理任务所共有的 GPIO 设备类的成员。

此概述讨论了以下主题：

- [GPIO 驱动程序支持概述](#gpio-driver-support-overview)
    - [GPIO 控制器驱动程序](#gpio-controller-drivers)
    - [使用 GPIO 插针的外围设备的驱动程序](#drivers-for-peripheral-devices-that-use-gpio-pins)

## <a name="gpio-controller-drivers"></a>GPIO 控制器驱动程序


硬件供应商提供驱动程序，以控制其 GPIO 控制器。 GPIO 控制器驱动程序是一个 KMDF 驱动程序，用于管理的 GPIO 控制器的所有特定于硬件的操作。 GPIO 控制器驱动程序配合 GpioClx 用于处理 I/O 请求的 GPIO 插针配置的组作为数据输入和输出数据。 此外，此驱动程序配合 GpioClx 以处理来自已配置为中断输入的 GPIO 插针的中断请求。

GPIO 控制器设备有一定数量的 GPIO 插针。 这些引脚可以以物理方式连接到外围设备。 GPIO 插针可配置为数据输入、 数据输出或中断请求输入。 通常情况下，专用于外围设备，并不由两个或多个设备共享 GPIO pin。 GPIO 插针和外围设备之间的连接固定的不能由用户更改 （例如，通过删除外围设备，并将它替换为另一台设备）。 因此，可以在平台固件中所述的 GPIO 插针到外围设备分配。




下图显示了 GPIO 控制器驱动程序和 GpioClx。

![gpio 组件的框图](images/gpiomodules.png)

GPIO 控制器驱动程序和 GpioClx 彼此通信通过 GpioClx 设备驱动程序接口 (DDI)。 GPIO 控制器驱动程序调用[驱动程序支持的方法](https://msdn.microsoft.com/library/windows/hardware/hh439460)实现的 GpioClx。 GpioClx 调用[事件的回调函数](https://msdn.microsoft.com/library/windows/hardware/hh439464)实现的 GPIO 控制器驱动程序。

GPIO 控制器驱动程序直接访问 GPIO 控制器设备的硬件寄存器。

GpioClx 处理来自以物理方式连接到 GPIO 插针的外围设备的驱动程序的 I/O 请求。 GpioClx 转化为简单的硬件操作，它通过调用由 GPIO 控制器驱动程序实现的回调函数的事件执行这些 I/O 请求。 例如，若要从中读取数据或将数据写入到一系列 GPIO 插针，GpioClx 调用事件的回调函数如[*客户端\_ReadGpioPins* ](https://msdn.microsoft.com/library/windows/hardware/hh439404)并[*客户端\_WriteGpioPins*](https://msdn.microsoft.com/library/windows/hardware/hh439439)。 GpioClx 管理 GPIO 控制器的 I/O 队列，从而使此任务的 GPIO 控制器驱动程序。

此外，GpioClx 处理从 GPIO 控制器设备的主中断，并将这些中断映射到辅助中断，由外围设备驱动程序处理。 主中断是由硬件设备生成的中断。 由操作系统以响应某些主中断生成辅助中断。 主要和次要中断进行全局系统中断 (GSIs) 标识。 ACPI 固件的硬件平台将 GSIs 分配给主中断，并在运行时，操作系统将 GSIs 分配给辅助中断。

例如，固件从 GPIO 控制器将 GSI 分配给硬件中断和操作系统 GSI 分配到配置为输入中断 GPIO 插针。

GpioClx 实现处理从 GPIO 控制器设备的硬件生成的主中断 ISR。 外围设备断言的 GPIO 插针，中断并在中断时此 pin 已启用并且其解除屏蔽、 GPIO 控制器中断处理器。 在响应中，内核的陷阱处理程序计划 GpioClx ISR 运行。 若要确定导致中断的 GPIO 插针，GpioClx ISR 调用[*客户端\_QueryActiveInterrupts* ](https://msdn.microsoft.com/library/windows/hardware/hh439395)事件回调函数，它将实现由 GPIO 控制器驱动程序。 GpioClx ISR 随后查找 GSI 分配给此 pin 并将此 GSI 传递给硬件抽象层 (HAL)。 HAL 通过调用此 GSI 注册 ISR 生成辅助中断。 此 ISR 属于原始添加中断外围设备的驱动程序。

有关主要和次要中断的详细信息，请参阅[GPIO 中断](https://msdn.microsoft.com/library/windows/hardware/hh406467)。

## <a name="drivers-for-peripheral-devices-that-use-gpio-pins"></a>使用 GPIO 插针的外围设备的驱动程序


在启动时，插即用 (PnP) 管理器枚举即插即用设备和非 PnP 设备。 对于具有固定的 GPIO 插针连接非 PnP 设备，即插即用管理器将查询平台固件，以确定作为向这些设备的系统管理硬件资源分配的 GPIO 插针。

外围设备的 KMDF 驱动程序收到其已分配的硬件资源期间[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调。 这些资源可能包括配置为数据输出、 数据输入或中断请求输入的 GPIO 插针。

GPIO I/O 资源是在 Windows 8 中新的 Windows 资源类型。 此资源包含的一个或多个 GPIO 插针可使用作为数据输入或数据输出。 如果外围设备驱动程序打开供读取的 GPIO I/O 资源，该驱动程序使用所有球瓶的资源中作为数据输入。 如果驱动程序将 GPIO I/O 资源打开用于写操作，该驱动程序使用所有球瓶的资源中作为数据输出。 有关演示如何将外围设备驱动程序打开与 GPIO I/O pin 的一组的逻辑连接的代码示例，请参阅以下主题：

[连接到 GPIO I/O 插针的 KMDF 驱动程序](https://msdn.microsoft.com/library/windows/hardware/hh406474)

配置为输入中断的 GPIO pin 作为普通 Windows 中断资源分配给驱动程序。 中断资源抽象隐藏这一事实而非等的可编程中断控制器 GPIO 插针，可能会实现中断。 因此，驱动程序可以视为基于 GPIO 的中断资源相同的任何其他中断资源。

若要访问 GPIO I/O 资源中的 GPIO 插针，外围设备驱动程序必须打开到球瓶的逻辑连接。 KMDF 驱动程序调用[ **WdfIoTargetOpen** ](https://msdn.microsoft.com/library/windows/hardware/ff548634)方法打开连接。 通过此连接，该驱动程序可以向的 GPIO 插针发送 I/O 请求。 该驱动程序发送[ **IOCTL\_GPIO\_读取\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/hh406483)请求以便从这些引脚读取数据 （如果它们是输入的 pin） 或[ **IOCTL\_GPIO\_编写\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/hh406487) （适用于输出插针） 将数据写入到它们的请求。

若要从在中断资源 GPIO 插针接收中断，外围设备驱动程序必须注册其中断服务例程 (ISR) 来实现此 pin 的中断资源从接收中断。 KMDF 驱动程序调用[ **WdfInterruptCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547345)方法连接到中断的 ISR。 

 

 




