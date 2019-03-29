---
title: 示例内核模式驱动程序
description: 示例内核模式驱动程序
ms.assetid: 09d08e07-e991-458f-aedf-018a0dd20af5
keywords:
- 内核模式驱动程序 WDK，示例
- 示例驱动程序 WDK 内核模式
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f3f0e910e2301eabc1383409205f8054d870f57
ms.sourcegitcommit: b13e6d44c71197971697f710c0ecb23db13fea91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57203934"
---
# <a name="sample-kernel-mode-drivers"></a>示例内核模式驱动程序

WDK 提供了各种示例内核模式驱动程序。 安装 WDK 后`src\general`子目录包含适用于所有内核模式驱动程序的示例驱动程序代码。 这些示例还维护联机。 这些示例包括：

[**DCHU**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)

适用 DCHU[设计原则](../develop/getting-started-with-universal-drivers.md)（声明性、 Componentized、 硬件支持应用程序 [HSA] 和通用 API 符合性）。  可以将它用作你自己的通用驱动程序包的模型。

[**PLX9x5x**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/PLX9x5x)

此示例演示如何编写使用 Windows 驱动程序框架的泛型 PCI 设备驱动程序。

[**SimpleMediaSource**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/SimpleMediaSource)

此示例演示如何创建可安装为相机和生成帧的自定义媒体源和驱动程序程序包。

[**SystemDma/wdm**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/SystemDma/wdm)

此示例演示 V3 系统 DMA 的使用情况。 它演示如何将驱动程序无法使用支持的 Windows 的系统 DMA 控制器将数据写入到使用 DMA 的硬件位置。

[**WinHEC 2017 Lab**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/WinHEC%202017%20Lab)

[**优化 WinHEC 2017/Windows 性能**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/WinHEC%202017/Optimizing%20Windows%20Performance)

[**cancel**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/cancel)  

演示如何使用[取消安全 IRP 队列](cancel-safe-irp-queues.md)。

[**echo**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/echo)

[**event**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/event)  

说明了内核模式驱动程序可以使用以通知应用程序的硬件事件，如果应用程序请求通知的方法。 一种方法使用[事件对象](event-objects.md)和其他依赖于[队列](queuing-and-dequeuing-irps.md)通知请求之前发生的事件。

[**filehistory**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/filehistory)

FileHistory 示例是一个控制台应用程序的启动文件历史记录服务，如果它已停止，并计划定期备份。 作为命令行参数，应用程序需要存储设备，以使用作为默认备份目标的路径名称。

[**IOCTL 示例**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/ioctl)

演示如何驱动程序应支持 I/O 控制代码。

[**obcallback**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/obcallback)

ObCallback 示例驱动程序演示如何使用已注册的回调过程保护。 该驱动程序注册在进程创建称为控件回调。

[**pcidrv**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/pcidrv)

此示例演示如何编写 PCI 设备的 KMDF 驱动程序。 示例工作原理与 Intel 82557/82558 基于 PCI 以太网适配器 (10/100) 和 Intel 兼容对象。

[**perfcounters/kcs**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/perfcounters/kcs)

Kcs 示例驱动程序演示如何使用内核模式性能库。

[**registry/regfltr**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/registry/regfltr)

RegFltr 示例演示如何编写注册表筛选器驱动程序。

[**toaster**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/toaster)  

为符合的驱动程序的一组提供的示例代码[Windows 驱动程序模型](windows-driver-model.md)(WDM)。 此示例还包括示例安装软件。

[**tracedrv**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)  

演示如何使用[WPP 软件跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556204)。

[**UMDF 驱动程序框架示例**](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/umdfSkeleton)

此示例演示如何使用版本 1 的用户模式驱动程序框架来编写最少驱动程序。

[**HID 设备的萤火虫 KMDF 筛选器驱动程序**](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/firefly)以及演示如何编写筛选器驱动程序，此示例演示如何使用远程 I/O 目标接口在内核模式下打开 HID 集合并发送 IOCTL 请求，以设置和获取功能报表，以及如何应用程序可以使用 WMI 接口将命令发送到筛选器驱动程序。

其他子目录`\src`目录包含为各种类型的硬件的内核模式驱动程序的示例代码。

## <a name="see-also"></a>请参阅

[Microsoft Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples)GitHub 上
