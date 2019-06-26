---
title: 体系结构和通过 I²C 传输的 HID 概述
description: 本部分介绍通过 I²C 传输支持 hid 标准的设备驱动程序堆栈。
ms.assetid: 99384729-552C-4847-AA35-E0D413018104
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d22cf5684dbb295f292c8b009041f64caae77f3c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375790"
---
# <a name="architecture-and-overview-for-hid-over-the-ic-transport"></a>体系结构和通过 I²C 传输的 HID 概述


本部分介绍通过 I²C 传输支持 hid 标准的设备驱动程序堆栈。

## <a name="architecture-and-overview"></a>体系结构和概述


HID I²C 驱动程序堆栈由现有和新组件提供由 Microsoft、 以及按 I²C 硅制造商提供的组件组成。 下图描绘了堆栈和以下组件。

![hid i2c 驱动程序堆栈通过](images/hid-i2c-arch.png)

Windows 8 提供了低功耗、 简单总线以有效地与操作系统进行通信的接口。 此接口被称为简单外围总线 （存储），并支持等 Inter-Integrated 线路 (I²C) 和串行外围设备接口 (SPI) 总线。 有关存储的其他详细信息，请参阅简单的外围总线主题。

Windows 8 提供了通过 I²C 实现 HID 协议规范的版本 1.0 基于 KMDF 的 HID 微型端口驱动程序。 此驱动程序名为 HIDI2C.sys。 Windows 将加载根据兼容 ID 匹配，高级配置和电源接口 (ACPI) 公开该驱动程序。 该驱动程序可确保使用 HID Ioctl 应用程序的应用程序级别利用 HID Ioctl 和 API 集的软件的兼容性。 它需要注意或包含数据时，设备将添加主机。 但是，该断言在执行之前，必须存在的 GPIO 连接。

**请注意**  HIDI2C.sys 设备驱动程序支持仅 I²C 总线。 它不在 Windows 8 中支持 SPI、 SMBUS 或其他低功耗总线。

 

## <a name="the-ic-controller-driver"></a>I²C 控制器驱动程序


I²C 控制器驱动程序公开一个串行外围总线 （存储） IOCTL 界面，用于执行读取和写入操作。 此驱动程序提供了实际控制器内部函数 (例如，I²C)。 存储类扩展，代表控制器驱动程序，处理与资源中心的所有交互，并实现必要的队列来管理同步目标。

**请注意**  HID I²C 驱动程序将无法在不具有兼容存储平台的 I²C 总线系统上。 请联系系统制造商联系，以确定是否兼容存储平台上的 I²C 总线上设备系统。

 

## <a name="the-gpio-controller-driver"></a>GPIO 控制器驱动程序


常规用途输入/输出 (GPIO) 控制器 GPIO 通过从设备传送中断。 这通常是使用 GPIO 插针的新数据的 Windows 或其他事件发出信号的简单从属组件。 GPIO 还可以控制设备 I²C 通道以外的方法。

## <a name="the-resource-hub"></a>资源中心


SoC 平台上的连接是通常无法发现的因为没有标准的设备 SoC.使用总线上的枚举 因此，这些设备必须以静态方式中的高级配置和电源接口 (ACPI) 定义。 此外，组件通常具有跨越多个总线，而不是严格的分支树结构的多个依赖项。

资源中心是管理所有设备和总线控制器间的连接的代理。 HIDI²C 驱动程序使用的资源中心以重新路由到相应的控制器驱动程序的设备打开请求。 有关资源中心的详细信息，请参阅[存储连接到设备的连接 Id](https://docs.microsoft.com/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices)主题。

 

 




