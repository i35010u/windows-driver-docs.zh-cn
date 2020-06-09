---
title: 基于 I i2c 传输的 HID 体系结构和概述
description: 本部分介绍了通过 I i2c 传输支持 HID 的设备的驱动程序堆栈。
ms.assetid: 99384729-552C-4847-AA35-E0D413018104
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df411e628dc8937c3d8cad6214758aa3c46b5d69
ms.sourcegitcommit: 188596c90e03a5619b5cbf0bff4276fc94777253
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84519846"
---
# <a name="architecture-and-overview-for-hid-over-the-ic-transport"></a>基于 I i2c 传输的 HID 体系结构和概述


本部分介绍了通过 I i2c 传输支持 HID 的设备的驱动程序堆栈。

## <a name="architecture-and-overview"></a>体系结构和概述


HID I i2c 驱动程序堆栈由 Microsoft 提供的现有和新组件以及由 I i2c 芯片制造商提供的组件组成。 下图描绘了堆栈和这些组件。

![基于 i2c 驱动程序堆栈的 hid](images/hid-i2c-arch.png)

Windows 8 提供了一个接口，用于实现低功率、简单的总线，以便与操作系统有效地通信。 此接口称为简单外围总线（SPB），它支持总线，如集成线路（I i2c）和串行外围设备接口（SPI）。 有关 SPB 的其他详细信息，请参阅简单外围总线主题。

Windows 8 提供了基于 KMDF 的 HID 微型端口驱动程序，该驱动程序实现了基于 I i2c 的 HID 协议规范的版本1.0。 此驱动程序名为 HIDI2C。 Windows 基于兼容的 ID 匹配（由高级配置和电源接口（ACPI）公开）加载此驱动程序。 驱动程序可确保对使用 hid IOCTLs 和 API 集的软件使用 HID IOCTLs 应用程序级别兼容性的应用。 当某个设备需要关注或包含数据时，它将断言该主机。 但是，在断言发生之前，GPIO 连接必须存在。

**注意**   HIDI2C 设备驱动程序仅支持 I i2c 总线。 它不支持在 Windows 8 中提供 SPI、SMBUS 或其他低功率总线。

 

## <a name="the-ic-controller-driver"></a>I i2c 控制器驱动程序


I i2c 控制器驱动程序公开串行外围总线（SPB） IOCTL 接口，以执行读写操作。 此驱动程序提供实际的控制器内部函数（例如，i2c）。 SPB 类扩展代表控制器驱动程序，可处理与资源中心的所有交互，并实现所需的队列来管理同时目标。

**注意**   在没有与 SPB 平台兼容的 i2c 总线的系统上，HID I i2c 驱动程序将不起作用。 请与系统制造商联系，以确定设备系统上的 i2c 总线是否与 SPB 平台兼容。

 

## <a name="the-gpio-controller-driver"></a>GPIO 控制器驱动程序


常规用途的输入/输出（GPIO）控制器通过 GPIO 传递设备发出的中断。 这通常是一个简单的从属组件，使用 GPIO pin 来向 Windows 发送新数据或其他事件的信号。 GPIO 还可以通过除 I i2c 通道以外的方法控制设备。

## <a name="the-resource-hub"></a>资源中心


SoC 平台上的连接通常是无法发现的，因为在 SoC 上使用的总线上没有用于设备枚举的标准。 因此，这些设备必须在高级配置和电源接口（ACPI）中静态定义。 而且，组件通常具有多个跨越多个总线的依赖项，而不是严格的分支树结构。

资源中心是管理所有设备和总线控制器间的连接的代理。 HIDI ²驱动程序使用资源中心将设备打开请求重新路由到相应的控制器驱动程序。 有关资源中心的详细信息，请参阅用于[SPB 连接的设备的连接 id](https://docs.microsoft.com/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices)主题。

 

 




