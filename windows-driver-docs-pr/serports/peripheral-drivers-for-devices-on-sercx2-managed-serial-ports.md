---
title: SerCx2 托管串行端口上的设备的外设驱动程序
description: 通常情况下，由 SerCx2 串行端口已永久连接到外围设备。
ms.assetid: 06412F66-3192-4D25-BDBA-FAB2211519DA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d346f2d1baba66ddd596dd0dba796ffb8b05ae1
ms.sourcegitcommit: 6a0636c33e28ce2a9a742bae20610f0f3435262c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2019
ms.locfileid: "65836348"
---
# <a name="peripheral-drivers-for-devices-on-sercx2-managed-serial-ports"></a>SerCx2 托管串行端口上的设备的外设驱动程序

通常情况下，由 SerCx2 串行端口已永久连接到外围设备。 此设备受将 I/O 请求发送到串行端口的外围设备驱动程序。 这些请求传输设备数据和配置的串行端口的状态。 由 SerCx2 和关联的串行控制器驱动程序，共同处理发送的外围设备驱动程序的 I/O 请求。

通常情况下，串行控制器芯片 (SoC) 集成线路上包含在系统中。 外围设备，它们可能连接到 SoC 芯片上的串行控制器的串行端口的示例包括 GPS、 无线 LAN、 相机和蓝牙设备。

按顺序连接的外围设备的外围设备驱动程序通常是[内核模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff544296)(KMDF) 或[用户模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff560442)(UMDF) 驱动程序。 若要与此设备进行通信，外围设备驱动程序必须首先打开串行控制器的逻辑连接并接收该驱动程序可以向其发送的 I/O 请求的文件句柄。 有关详细信息，请参阅[打开 SerCx2-Managed 串行端口](opening-a-sercx2-managed-serial-port.md)。

**此页上**

- [串行驱动程序体系结构](#serial-driver-architecture)
- [I/O 请求路径](#i-o-request-path)
- [中断路径](#interrupt-path)

## <a name="serial-driver-architecture"></a>串行驱动程序体系结构

以下块图显示窗体 （在关系图的底部） 外围设备和此设备的 （在关系图的顶部） 的外围设备驱动程序之间的通信路径的软件和硬件层。 在此示例中，外围设备连接到串行控制器上的端口和 GPIO 控制器上的中断 pin。

![外围设备 sercx2 托管的串行端口上的软件和硬件层](images/seriallayers.png)

在此示例中的外围设备驱动程序是将输入/输出请求发送到外围设备 UMDF 驱动程序。 这些请求将经历左侧和右侧的关系图上显示的通信路径。 由 SerCx2 和串行控制器驱动程序处理请求。 外围设备驱动程序可以请求设置串行端口的硬件配置的 I/O 操作 （例如，将更改的波特率） 和传输数据传入和传出的串行端口通过在外围设备。 有关详细信息，请参阅[I/O 请求路径](#i-o-request-path)。

从外围设备旅行向上通过通信路径上图右侧会中断。 在此关系图的右下角所示，外围设备的中断插针连接到常规用途的 I/O (GPIO) 控制器上的 pin。 此 GPIO pin 配置为从外围设备接收中断信号。 在 SoC 基于硬件的平台，GPIO 控制器经常扮演可编程中断控制器的角色。 有关详细信息，请参阅[中断路径](#interrupt-path)。

在关系图中以灰色显示的两个块都是系统提供的模块。 可从 Windows 8 开始 GPIO 框架扩展 (GpioClx)。 如 SerCx2，GpioClx 是 KMDF 的扩展。 GpioClx 执行所共有的 GPIO 控制器的各种功能。 GpioClx 适用于管理 GPIO 控制器中的所有特定于硬件的操作的 GPIO 控制器驱动程序。 有关详细信息，请参阅[GPIO 驱动程序支持概述](https://msdn.microsoft.com/library/windows/hardware/hh439512)。

## <a name="i-o-request-path"></a>O 请求路径

若要将数据传输到外围设备，外围设备驱动程序，将发送执行写入操作 ([**IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff546904)) 到串行控制器的请求。 若要从外围设备接收数据，外围设备驱动程序，将发送读取 ([**IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff546883)) 到串行控制器的请求。

此外，Windows 定义外围设备驱动程序可用于执行各种特定于串行控制器的 I/O 控制操作的设备 I/O 控制请求 (Ioctl) 的一组。 外围设备驱动程序可以请求的 I/O 控制操作的示例如下：

- 设置串行端口的传输和接收数据的波特率。
- 设置的超时间隔的读取和写入请求。
- 指定一组硬件事件在其外围设备驱动程序将收到通知的串行端口。

SerCx2 支持许多相同的串行 Ioctl 收件箱串行驱动程序、 Serial.sys，和版本 1 的串行框架扩展 (SerCx)。 获取详细信息：

- 请参阅中的表[串行 I/O 请求接口](serial-i-o-request-interface.md)确定 SerCx2 是否支持特定的串行 IOCTL。
- 请参阅[串行设备控制请求](https://msdn.microsoft.com/library/windows/hardware/ff547466)有关由 Windows 串行 I/O 请求接口定义的所有串行 Ioctl 的详细说明。
- 请参阅[串行控制器驱动程序概述](serial-drivers-overview.md)有关 Serial.sys、 SerCx 和 SerCx2 的简要介绍。

## <a name="interrupt-path"></a>中断路径

如中所示[串行驱动程序体系结构](#serial-driver-architecture)关系图中，外围设备使用 GPIO pin 将发送设备中断到外围设备驱动程序。 在外围设备的中断信号响应，GPIO 控制器发出信号的硬件中断 (称为*主*中断) 处理器。 操作系统将定向到 GpioClx 的 ISR.此中断 接下来，GpioClx 标识导致中断，哪个 GPIO pin 并查找虚拟中断的全球系统中断 (GSI) 标识符 (称为*辅助*中断) 从外围设备。 GpioClx 提供对 HAL 和 HAL GSI 调用外围设备驱动程序的 ISR. 若要处理中断，外围设备驱动程序通常将一个或多个 I/O 请求发送到外围设备通过 SerCx2 和串行控制器驱动程序。 有关主要和次要中断的详细信息，请参阅[GPIO 中断](https://msdn.microsoft.com/library/windows/hardware/hh406467)。

GPIO 中断是外围设备驱动程序在外围设备接收通知的硬件事件只有一种方法。 另一种方法是外围设备驱动程序的请求将通知从 SerCx2 和串行控制器驱动程序时在串行端口上发生某些类型的硬件事件。 例如，外围设备驱动程序可要求在串行控制器接收的外围设备的串行数据时获得通知。 若要请求这些通知，外围设备驱动程序将发送[ **IOCTL\_串行\_设置\_等待\_掩码**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_wait_mask)到外围设备的请求若要指定一组事件来监视，然后将发送[ **IOCTL\_串行\_等待\_ON\_掩码**](https://msdn.microsoft.com/library/windows/hardware/ff546805)开始侦听请求这些事件。 这些请求都由 SerCx2，处理在串行控制器驱动程序的帮助。 有关外围设备驱动程序可以监视的事件类型的详细信息，请参阅**串行\_EV\_* XXX*** 描述了这些[ **IOCTL\_序列\_设置\_等待\_掩码**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_wait_mask)。

但是，串行控制器可以检测到硬件事件只能处于 D0 设备电源状态时。 如果串行控制器在低功耗状态，外围设备驱动程序不能依赖于从串行控制器的通知时，例如，外围设备有新的驱动程序读取数据。 在这种情况下，外围设备必须通过 GPIO pin 发送中断信号 （或这样一来，唤醒信号）。 GPIO 控制器耗电非常少，通常会一直保持活动状态后大多数其他设备已进入低功耗状态。
