---
title: 相机驱动程序示例
description: 此目录中的示例编写你的设备的自定义驱动程序提供一个起始点。
ms.assetid: C5DC72F1-D093-47D0-9AC3-680878C5A868
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7660536daeff45e57cf012ca7aa791c59ac9c664
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356755"
---
# <a name="general-driver-samples"></a>相机驱动程序示例


此目录中的示例编写你的设备的自定义驱动程序提供一个起始点。

## <a name="general-samples"></a>一般示例


| 示例名称                     | 解决方案                                                              | 描述                                                                                                                                                                                                                                        |
|---------------------------------|-----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 取消安全 IRP 队列           | [cancel](https://go.microsoft.com/fwlink/p/?LinkId=617705)             | 演示如何使用取消安全队列例程 IoCsqInitialize，IoCsqInsertIrp、 IoCsqRemoveIrp、 IoCsqRemoveNextIrp。 通过使用这些例程，驱动程序开发人员不必担心 IRP 取消争用条件。                |
| KMDF Echo                       | [kmdfecho](https://go.microsoft.com/fwlink/p/?LinkId=617706)           | 演示如何使用顺序队列序列化读取和写入请求提供给该驱动程序。                                                                                                                                           |
| UMDF Echo                       | [echo](https://go.microsoft.com/fwlink/p/?LinkId=617707)               | 演示如何使用 UMDF 1，若要编写驱动程序，并采用最佳实践。                                                                                                                                                                     |
| UMDF2 Echo                      | [umdf2echo](https://go.microsoft.com/fwlink/p/?LinkId=617708)          | 演示如何使用 UMDF 2 来编写驱动程序，并采用最佳实践。                                                                                                                                                                     |
| UMDF SocketEcho                 | [umdfsocketecho](https://go.microsoft.com/fwlink/p/?LinkId=617709)     | 演示如何使用 UMDF 编写驱动程序，演示最佳做法。                                                                                                                                                                |
| 硬件事件                  | [eventsample](https://go.microsoft.com/fwlink/p/?LinkId=617711)        | 演示两种不同方式的内核模式驱动程序可以通知有关硬件事件的应用程序。 一种方法使用基于事件的方法，和另一个则使用基于 IRP 的方法。 示例驱动程序使用计时器 DPC 模拟硬件事件。 |
| 文件历史记录                    | [filehistory](https://go.microsoft.com/fwlink/p/?LinkId=617712)        | 如果它已停止，并计划定期备份启动文件历史记录服务，一个控制台应用程序。                                                                                                                                       |
| WDF 安装包        | [installwdf](https://go.microsoft.com/fwlink/p/?LinkId=617713)         | 演示如何在系统上安装 WDF 包。 此代码可用作-是安装到用户系统上所需的 WDF 组件。 示例代码还重写到现有的安装程序应用程序，以提供更好的体验。 |
| 非 PnP 驱动程序示例           | [ioctl](https://go.microsoft.com/fwlink/p/?LinkId=620307)              | 演示如何编写非 PnP 驱动程序使用内核模式驱动程序框架。                                                                                                                                                                 |
| IOCTL                           | [ioctl](https://go.microsoft.com/fwlink/p/?LinkId=617715)              | 演示如何使用四种不同类型的 Ioctl (方法\_IN\_直接、 方法\_OUT\_DIRECT，方法\_NEITHER，和方法\_缓冲)。                                                                                                         |
| ObCallback                      | [obcallback](https://go.microsoft.com/fwlink/p/?LinkId=617716)         | 演示如何将已注册的回调过程保护。 该驱动程序注册在进程创建称为控件回调。                                                                                                  |
| PCIDRV                          | [pcidrv](https://go.microsoft.com/fwlink/p/?LinkId=617717)             | 此示例演示如何编写 PCI 设备的 KMDF 驱动程序。 示例工作原理与 Intel 82557/82558 基于 PCI 以太网适配器 (10/100) 和 Intel 兼容对象。                                                                       |
| 内核计数器                  | [kcs](https://go.microsoft.com/fwlink/p/?LinkId=617718)                | 演示如何使用内核模式性能库。 该驱动程序不会控制任何硬件;它只需提供的计数器。 该代码包含用于说明每个函数作用的注释。                                                 |
| PLX9x5x PCI 驱动程序              | [PLX9x5x](https://go.microsoft.com/fwlink/p/?LinkId=617719)            | 演示如何编写使用 Windows 驱动程序框架 (WDF) 的泛型 PCI 设备驱动程序。 此驱动程序的目标硬件是 PLX9656/9653RDK LITE 板。                                                                                |
| RegFltr                         | [regflltr](https://go.microsoft.com/fwlink/p/?LinkId=617720)           | 演示如何编写注册表筛选器驱动程序。                                                                                                                                                                                                       |
| 系统 DMA                      | [SystemDma](https://go.microsoft.com/fwlink/p/?LinkId=617722)          | 演示 V3 系统 DMA 的使用情况。 它演示如何将驱动程序无法使用支持的 Windows 的系统 DMA 控制器将数据写入到使用 DMA 的硬件位置。                                                                              |
| Toaster 示例驱动程序           | [toaster](https://go.microsoft.com/fwlink/p/?LinkId=620309)            | 一系列重复的演示的内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 版本 1 的 Windows 驱动程序开发的基本方面的示例。                                                    |
| Toaster 程序包示例          | [toastpkg](https://go.microsoft.com/fwlink/p/?LinkId=617723)           | 模拟的 toaster 示例驱动程序硬件第一个和第一个软件的安装。                                                                                                                                                             |
| Toaster 示例 （UMDF 版本 2） | [umdf2toaster](https://go.microsoft.com/fwlink/p/?LinkId=620310)       | 一系列重复的示例演示如何使用用户模式驱动程序框架 (UMDF) 版本 2 的 Windows 驱动程序开发的基本情况。                                                                                               |
| EventDrv                        | [evntdrv](https://go.microsoft.com/fwlink/p/?LinkId=617724)            | 内核模式跟踪提供程序和驱动程序。 该驱动程序不会控制任何硬件;它只是生成跟踪事件。 它旨在演示了如何使用的事件跟踪 Windows (ETW) API 在驱动程序。                                 |
| 系统跟踪控件            | [SystemTraceControl](https://go.microsoft.com/fwlink/p/?LinkId=617725) | 演示如何使用事件跟踪控制 Api 从系统跟踪提供程序收集事件。                                                                                                                                               |
| tracedrv                        | [tracedrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)           | 检测软件跟踪的一个示例驱动程序。                                                                                                                                                                                                 |
| UMDF 驱动程序框架            | [umdfSkeleton](https://go.microsoft.com/fwlink/p/?LinkId=617727)       | 演示如何使用用户模式驱动程序框架来编写最少驱动程序，并演示最佳做法。                                                                                                                                         |

 

 

 




