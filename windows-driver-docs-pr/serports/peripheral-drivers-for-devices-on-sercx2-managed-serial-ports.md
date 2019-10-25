---
title: SerCx2 托管串行端口上的设备的外设驱动程序
description: 通常，由 SerCx2 管理的串行端口会永久连接到外围设备。
ms.assetid: 06412F66-3192-4D25-BDBA-FAB2211519DA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 255ccc3272eb13935b38e0d5342b7c75d0c11b1a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844945"
---
# <a name="peripheral-drivers-for-devices-on-sercx2-managed-serial-ports"></a>SerCx2 托管串行端口上的设备的外设驱动程序

通常，由 SerCx2 管理的串行端口会永久连接到外围设备。 此设备由向串行端口发送 i/o 请求的外围设备驱动程序控制。 这些请求将数据传入和传出设备，并配置串行端口的状态。 外设驱动程序发送的 i/o 请求由 SerCx2 和关联的串行控制器驱动程序共同处理。

通常，串行控制器包含在芯片（SoC）集成线路上的系统中。 可能连接到 SoC 芯片上串行控制器串行端口的外围设备的示例包括 GPS、无线 LAN、照相机和蓝牙设备。

串行连接外围设备的外围设备驱动程序通常是一个[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)（KMDF）或[用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)（UMDF）驱动程序。 要与此设备通信，外设驱动程序必须首先打开与串行控制器的逻辑连接，并接收驱动程序可向其发送 i/o 请求的文件句柄。 有关详细信息，请参阅[打开 SerCx2 管理的串行端口](opening-a-sercx2-managed-serial-port.md)。

**在此页上**

- [串行驱动程序体系结构](#serial-driver-architecture)
- [I/o 请求路径](#i-o-request-path)
- [中断路径](#interrupt-path)

## <a name="serial-driver-architecture"></a>串行驱动程序体系结构

以下块示意图显示了构成外围设备（在关系图底部）与此设备的外围设备驱动程序（位于关系图顶部）之间的通信路径的软件和硬件层。 在此示例中，外围设备连接到串行控制器上的端口和 GPIO 控制器上的中断端口。

![sercx2 管理的串行端口上的外围设备的软件和硬件层](images/seriallayers.png)

此示例中的外围设备驱动程序是将 i/o 请求发送到外围设备的 UMDF 驱动程序。 这些请求通过关系图左侧显示的通信路径移动。 请求由 SerCx2 和串行控制器驱动程序处理。 外设驱动程序可以请求设置串行端口的硬件配置的 i/o 操作（例如，更改波特率），并通过串行端口将数据传入和传出外围设备。 有关详细信息，请参阅[i/o 请求路径](#i-o-request-path)。

从外围设备的中断通过上图右侧的通信路径向后移动。 如此图的右下角所示，外围设备的中断 pin 连接到常规用途 i/o （GPIO）控制器上的 pin。 此 GPIO pin 配置为接收来自外围设备的中断信号。 在基于 SoC 的硬件平台中，GPIO 控制器经常扮演可编程中断控制器的角色。 有关详细信息，请参阅[中断路径](#interrupt-path)。

图中以灰色显示的两个块是系统提供的模块。 从 Windows 8 开始，使用 GPIO framework 扩展（GpioClx）。 与 SerCx2 一样，GpioClx 是对 KMDF 的扩展。 GpioClx 执行各种 GPIO 控制器通用的功能。 GpioClx 适用于 GPIO 控制器驱动程序，该驱动程序管理 GPIO 控制器中所有特定于硬件的操作。 有关详细信息，请参阅[GPIO 驱动程序支持概述](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview)。

## <a name="i-o-request-path"></a>I O 请求路径

若要将数据传输到外围设备，外围设备驱动程序会向串行控制器发送写入（[**IRP\_MJ\_写入**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))）请求。 若要从外围设备接收数据，外围设备驱动程序会向串行控制器发送读取（[**IRP\_MJ\_读取**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))）请求。

此外，Windows 定义了一组设备 i/o 控制请求（IOCTLs），外设驱动程序可以使用这些请求来执行特定于串行控制器的各种 i/o 控制操作。 以下是外设驱动程序可以请求的 i/o 控制操作的示例：

- 设置串行端口传输和接收数据的波特率。
- 设置读和写请求的超时间隔。
- 在串行端口指定一组硬件事件，外围设备驱动程序接收通知。

SerCx2 支持的多个串行 IOCTLs 与串行框架扩展（SerCx）的收件箱串行驱动程序、Serial 和版本1相同。 有关详细信息：

- 请参阅[串行 I/o 请求接口](serial-i-o-request-interface.md)中的表，以确定 SerCx2 是否支持特定的序列 IOCTL。
- 有关 Windows 串行 i/o 请求接口定义的所有串行 IOCTLs 的详细说明，请参阅[串行设备控制请求](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。
- 有关 SerCx 和 SerCx2 的简要介绍，请参阅[串行控制器驱动程序概述](serial-drivers-overview.md)。

## <a name="interrupt-path"></a>中断路径

如[串行驱动程序体系结构](#serial-driver-architecture)关系图中所示，外围设备使用 GPIO pin 将设备中断发送到外围设备驱动程序。 为了响应来自外围设备的中断信号，GPIO 控制器向处理器发出硬件中断（称为*主*中断）。 操作系统将此中断定向到 GpioClx 的 ISR。 接下来，GpioClx 标识哪个 GPIO pin 导致了中断，并从外围设备中查找虚拟中断（称为*辅助*中断）的全局系统中断（GSI）标识符。 GpioClx 向 HAL 提供 GSI，HAL 会调用外围设备驱动程序的 ISR。 为了处理中断，外围设备驱动程序通常通过 SerCx2 和串行控制器驱动程序向外围设备发送一个或多个 i/o 请求。 有关主要和次要中断的详细信息，请参阅[GPIO 中断](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)。

GPIO 中断只是外设驱动程序在外围设备中接收硬件事件通知的一种方法。 另一种方法是，当串行端口出现特定类型的硬件事件时，外围设备驱动程序从 SerCx2 和串行控制器驱动程序请求通知。 例如，当串行控制器从外围设备接收串行数据时，外设驱动程序可以请求通知。 若要请求这些通知，外围设备驱动程序会向外围设备发送[**ioctl\_串行\_集\_\_等待**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_wait_mask)向外围设备指定一组事件，然后将[**IOCTL 发送\_串行\_等待\_\_MASK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_wait_on_mask)请求开始侦听这些事件。 这些请求是通过串行控制器驱动程序的帮助来处理的 SerCx2。 有关外围设备驱动程序可以监视的事件类型的详细信息，请参阅在[**IOCTL\_串行\_设置\_等待\_掩码**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_wait_mask)中描述的**串行\_EV\_* XXX***。

但串行控制器只能检测到处于 D0 设备电源状态的硬件事件。 如果串行控制器处于低功耗状态，则外围设备驱动程序无法依赖于串行控制器的通知来了解何时，例如外围设备包含要读取的驱动程序的新数据。 在这种情况下，外围设备必须通过 GPIO pin 发送中断信号（也可能是唤醒信号）。 GPIO 控制器使用非常少的电源，通常在大多数其他设备进入低功耗状态后保持活动状态。
