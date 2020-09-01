---
title: 示例内核模式驱动程序
description: 示例内核模式驱动程序
ms.assetid: 09d08e07-e991-458f-aedf-018a0dd20af5
keywords:
- 内核模式驱动程序 WDK，示例
- 示例驱动程序 WDK 内核模式
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca84d3ddff0af71eecbb23c8e3bc5563be517aae
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185119"
---
# <a name="sample-kernel-mode-drivers"></a>示例内核模式驱动程序

WDK 提供各种示例内核模式驱动程序。 安装 WDK 后， `src\general` 子目录包含适用于所有内核模式驱动程序的示例驱动程序代码。 这些示例还会联机维护。 这些示例包括：

[**DCHU**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)

 (声明性、组件化和硬件支持应用 [HSA] ) 应用 DCH [设计原则](../develop/getting-started-with-windows-drivers.md) 。  可以将其用作自己的 Windows 驱动程序包的模型。

[**PLX9x5x**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/PLX9x5x)

此示例演示如何使用 Windows 驱动程序框架为通用 PCI 设备编写驱动程序。

[**SimpleMediaSource**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/SimpleMediaSource)

此示例演示如何创建可作为照相机安装的自定义媒体源和驱动程序包，并生成帧。

[**SystemDma/wdm**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/SystemDma/wdm)

此示例演示如何使用 V3 系统 DMA。 其中显示了驱动程序如何使用 Windows 支持的系统 DMA 控制器将数据写入到使用 DMA 的硬件位置。

[**WinHEC 2017 实验室**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/WinHEC%202017%20Lab)

[**WinHEC 2017/优化 Windows 性能**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/WinHEC%202017/Optimizing%20Windows%20Performance)

[**取消**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/cancel)  

演示如何使用 [取消安全 IRP 队列](cancel-safe-irp-queues.md)。

[echo](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo)

[**引发**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/event)  

演示当应用程序请求通知时，内核模式驱动程序可用于向应用程序通知硬件事件的技术。 一种方法使用 [事件对象](event-objects.md) ，另一种方法依赖于在事件发生之前对通知请求进行 [排队](queuing-and-dequeuing-irps.md) 。

[**filehistory**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/filehistory)

FileHistory 示例是一个控制台应用程序，它会启动文件历史记录服务（如果已停止），并计划定期备份。 应用程序需要使用作为默认备份目标的存储设备的路径名称作为命令行参数。

[**IOCTL 示例**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/ioctl)

演示驱动程序应如何支持 i/o 控制代码。

[**obcallback**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/obcallback)

ObCallback 示例驱动程序演示如何使用注册的回调来实现进程保护。 驱动程序将注册在进程创建时调用的控件回调。

[**pcidrv**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/pcidrv)

此示例演示如何为 PCI 设备编写 KMDF 驱动程序。 此示例适用于基于 Intel 82557/82558 的 PCI 以太网适配器 (10/100) 和 Intel 兼容机。

[**perfcounters/kcs**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/perfcounters/kcs)

Kcs 示例驱动程序演示内核模式性能库的使用。

[**注册表/regfltr**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/registry/regfltr)

RegFltr 示例演示如何编写注册表筛选器驱动程序。

[**吐司炉**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster)  

提供一组符合 [Windows 驱动模型](windows-driver-model.md) (WDM) 的驱动程序的示例代码。 此示例还包括示例安装软件。

[**tracedrv**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)  

演示如何使用 [WPP 软件跟踪](../devtest/wpp-software-tracing.md)。

[**UMDF 驱动程序主干示例**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/umdfSkeleton)

此示例演示如何使用用户模式驱动程序框架的第1版来编写最小的驱动程序。

[**HID 设备的 FIREFLY KMDF 筛选器驱动程序**](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/firefly) 除了说明如何编写筛选器驱动程序外，此示例还演示如何使用远程 i/o 目标接口以内核模式打开 HID 集合，并发送 IOCTL 请求来设置和获取功能报告，以及应用程序如何使用 WMI 接口将命令发送到筛选器驱动程序。

目录的其他子目录 `\src` 包含用于各种硬件类型的内核模式驱动程序的示例代码。

## <a name="see-also"></a>请参阅

GitHub 上的[Microsoft Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples)