---
title: 相机驱动程序示例
description: 此目录中的示例提供了为设备编写自定义驱动程序的起点。
ms.assetid: C5DC72F1-D093-47D0-9AC3-680878C5A868
ms.date: 12/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: ea54e92fb10af5534b82926058923d571249dce5
ms.sourcegitcommit: 30fa63ad13fd5e2e883b76a44f0703e01049ffa1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74735263"
---
# <a name="general-driver-samples"></a>相机驱动程序示例

此目录中的示例提供了为设备编写自定义驱动程序的起点。

| 示例 | 描述 |
| --- | --- |
| [取消安全 IRP 队列](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/cancel-safe-irp-queue-sample) | 演示如何使用取消安全队列例程 IoCsqInitialize、IoCsqInsertIrp、IoCsqRemoveIrp、IoCsqRemoveNextIrp。 使用这些例程，驱动程序开发人员无需担心 IRP 取消争用情况。 |
| [KMDF Echo](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/kmdf-echo-sample) | 演示如何使用顺序队列来序列化提供给驱动程序的读取和写入请求。 |
| [UMDF1 Echo](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/echo-sample-umdf-version-1) | 演示如何使用 UMDF 1 编写驱动程序并使用最佳做法。 |
| [UMDF2 Echo](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/echo-sample-umdf-version-2) | 演示如何使用 UMDF 2 编写驱动程序并使用最佳做法。 |
| [UMDF SocketEcho 示例（UMDF 版本1）](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/umdf-socketecho-sample-umdf-version-1) | 演示如何使用 UMDF 编写驱动程序并演示最佳做法。 |
| [硬件事件](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/hardware-event-sample)| 演示内核模式驱动程序可以通过两种不同的方式向应用程序通知有关硬件事件的方法。 一种方法使用基于事件的方法，另一种方法使用基于 IRP 的方法。 示例驱动程序使用计时器 DPC 来模拟硬件事件。 |
| [文件历史记录](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/file-history-sample)| 一种控制台应用程序，该应用程序启动文件历史记录服务（如果已停止）并计划定期备份。 |
| [非 PnP 驱动程序示例](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/non-pnp-driver-sample)| 演示如何使用内核模式驱动程序框架编写非 PnP 驱动程序。 |
| [IOCTL](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/ioctl)| 演示如何使用四种不同类型的 IOCTLs （方法\_\_直接、方法\_OUT\_直接、方法\_和\_缓存的方法。 |
| [ObCallback](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/obcallback-callback-registration-driver) | 演示如何使用注册的回调来实现进程保护。 驱动程序将注册在进程创建时调用的控件回调。 |
| [PCIDRV](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/pcidrv---wdf-driver-for-pci-device) | 此示例演示如何为 PCI 设备编写 KMDF 驱动程序。 此示例适用于基于 Intel 82557/82558 的 PCI 以太网适配器（10/100）和 Intel 兼容机。 |
| [内核计数器](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/kernel-counter-sample-kcs) | 演示内核模式性能库的使用。 该驱动程序不控制任何硬件，只是提供计数器。 代码包含注释，用于说明每个函数的作用。 |
| [PLX9x5x PCI 驱动程序](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/plx9x5x-pci-driver) | 演示如何使用 Windows 驱动程序框架（WDF）为通用 PCI 设备编写驱动程序。 此驱动程序的目标硬件为 PLX9656/9653RDK。 |
| [RegFltr](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/regfltr-sample-driver) | 说明如何编写注册表筛选器驱动程序。 |
| [简单媒体源](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/simplemediasource-sample) | 演示如何编写自定义媒体源和驱动程序包。 |
| [系统 DMA](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/system-dma) | 演示 V3 系统 DMA 的用法。 其中显示了驱动程序如何使用 Windows 支持的系统 DMA 控制器将数据写入到使用 DMA 的硬件位置。 |
| [Toaster 示例驱动程序](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/toaster-sample-driver) | 一系列迭代的示例，演示了内核模式驱动程序框架（KMDF）和用户模式驱动程序框架（UMDF）版本1的 Windows 驱动程序开发的基础知识。 |
| [Toaster 包示例](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/toaster-package-sample-driver) | 模拟 toaster 示例驱动程序的硬件优先和软件优先安装。 |
| [Toaster 示例（UMDF 版本2）](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/toaster-sample-umdf-version-2) | 一系列使用用户模式驱动程序框架（UMDF）版本2演示 Windows 驱动程序开发的基本方面的示例。 |
| [EventDrv](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/eventdrv) | 内核模式跟踪提供程序和驱动程序。 该驱动程序不控制任何硬件;它只是生成跟踪事件。 它旨在演示如何使用驱动程序中的 Windows 事件跟踪（ETW） API。 |
| [系统跟踪控制](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/systemtraceprovider) | 演示如何使用事件跟踪控制 Api 从系统跟踪提供程序收集事件。 |
| [Tracedrv](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/tracedrv) | 为软件跟踪检测的示例驱动程序。|
| [UMDF 驱动程序主干](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/umdf-driver-skeleton-sample-umdf-version-1) | 演示如何使用用户模式驱动程序框架编写最小的驱动程序并显示最佳实践。 |
| [适用于通用驱动程序的驱动程序包安装工具包](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/driver-package-installation-toolkit-for-universal-drivers) | 说明通用驱动程序设计的 DCHU 原则。 |
| [WinHEC 2017 实验室](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/winhec-2017-lab) | WinHEC 2017 实验室中的 Toaster 示例： Toaster 驱动程序、PlugInToaster 和 Toaster 支持应用程序。 |
