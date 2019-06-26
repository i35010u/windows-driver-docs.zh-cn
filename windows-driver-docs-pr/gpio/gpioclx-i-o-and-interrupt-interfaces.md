---
title: GpioClx I/O 和中断接口
description: 通常情况下，GPIO 控制器的客户端是连接到 GPIO 引脚的外围设备的驱动程序。
ms.assetid: F75E9B21-9DA4-4DD9-BB44-59E19EDFC099
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb94a00384f9b4caf47ecccd3f2c4e023918a337
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363587"
---
# <a name="gpioclx-io-and-interrupt-interfaces"></a>GpioClx I/O 和中断接口


通常情况下，GPIO 控制器的客户端是连接到 GPIO 引脚的外围设备的驱动程序。 这些驱动程序使用 GPIO 引脚作为低带宽数据通道、设备选择器输出和中断请求输入。 外围设备驱动程序打开到 GPIO 引脚的逻辑连接，这些引脚已配置为数据输入或输出。 它们使用这些连接将 I/O 请求发送到这些引脚。 另外，外围设备驱动程序可以通过逻辑方式将其中断服务例程连接到已配置为中断请求输入的 GPIO 引脚。

GPIO 插针是系统管理硬件资源。 外围设备驱动程序启动其设备之前，插即用 (PnP) 管理器将分配给此驱动程序的硬件资源的列表。 此列表中的硬件资源可能包括：

-   GPIO I/O 资源。 此资源是一组的一个或多个 GPIO 固定配置为数据输入或数据输出。 GPIO I/O 资源是从 Windows 8 开始新的 Windows 资源类型。
-   中断。 此中断资源可能实现作为 GPIO pin 配置为中断输入，但它可能在可编程中断控制器还是专用的中断 pin 上处理器包作为改为实现。 硬件抽象层 (HAL) 中断抽象隐藏这些实现的详细信息，可以放心地忽略哪些客户端驱动程序。

外围设备驱动程序可以作为数据输入或输出中使用的 GPIO 插针的一组之前，该驱动程序必须打开这些引脚的逻辑连接。 例如，[内核模式驱动程序接口](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(KMDF) 驱动程序将获取 WDFIOTARGET 句柄来标识连接。 驱动程序使用此句柄将 I/O 请求发送到球瓶。 具体而言，客户端驱动程序发送[ **IOCTL\_GPIO\_编写\_PIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpio/ni-gpio-ioctl_gpio_write_pins)并[ **IOCTL\_GPIO\_读取\_插针**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpio/ni-gpio-ioctl_gpio_read_pins) I/O 控制请求以将数据写入到输出插针和输入插针从读取数据。 有关代码示例演示如何连接到一系列 GPIO I/O pin，请参阅以下主题：

[连接到 GPIO I/O 插针的 KMDF 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/gpio/connecting-a-kmdf-driver-to-gpio-i-o-pins)

若要使用的中断资源接收中断，外围设备驱动程序从逻辑上必须与该中断连接中断服务例程 (ISR)。 例如，内核模式驱动程序可以使此连接，通过调用[ **WdfInterruptCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)方法或[ **IoConnectInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)例程。 在连接后，驱动程序的 ISR 在运行时外围设备发出信号的中断请求到输入的 GPIO 插针或中断控制器。 有关中断的详细信息，请参阅[创建中断对象](https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-an-interrupt-object)。

GPIO framework 扩展 (GpioClx) 可用于管理 I/O 连接和外围设备驱动程序作为其客户端的中断连接。 PnP 管理器可能将不同的 GPIO 插针上 GPIO 控制器设备组分配给不同的客户端驱动程序。 这些引脚的一些配置为数据输入或输出，以及一些配置为中断请求输入。

当客户端驱动程序收到中断请求或将 I/O 请求发送到 GPIO 插针，GpioClx 调用事件回叫函数，由 GPIO 控制器驱动程序实现。 这些回调访问 GPIO 控制器设备中的硬件寄存器。 通过调用这些函数，GpioClx 读取数据输入、 输出，将数据写入和中断请求 （通过查询、 启用、 屏蔽、 清除，并管理等等，配置为中断输入的 GPIO 插针）。

GpioClx 执行管理 I/O 和中断的客户端打开连接所需的所有处理。 GPIO 控制器驱动程序，通过将这些 GpioClx 到连接的管理委派 — 仅负责访问 GPIO 控制器设备中的硬件寄存器的相对简单的任务。 GPIO 控制器驱动程序不需要知道为其进行特定访问权限的客户端驱动程序。

 

 




