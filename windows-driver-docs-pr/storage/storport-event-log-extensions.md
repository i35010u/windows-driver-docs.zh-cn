---
title: Storport 事件日志扩展
description: Storport 事件日志扩展
ms.assetid: 03b0bdef-cefa-4ad8-b9bf-a5f6b5f64cc6
ms.date: 06/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: 71fdff09578d4c456f9f95e95e6051d64a0c1e98
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844476"
---
# <a name="storport-event-log-extensions"></a>Storport 事件日志扩展

与许多其他类型的驱动程序一样，Storport 微型端口驱动程序必须在系统事件日志中创建条目，以使管理员能够了解连接存储设备的情况。 通常会创建这些事件日志条目，以响应与设备相关的故障。 还可以记录事件以进行遥测、调试和优化。

尽管 Windows 内核本身提供了一个灵活的接口来创建事件日志条目，但 Storport 微型端口模型不允许微型端口驱动程序直接访问该接口。 相反，Storport 提供了一个围绕内核系统事件日志工具的包装，微型端口驱动程序使用包装器来创建事件日志条目。

具体而言，Storport 提供以下事件日志例程：

* [**StorPortLogTelemetryEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportlogtelemetryex)允许微型端口使用微型端口自定义数据（Windows 10 1903 版及更高版本）记录 tracelogging 度量值或遥测事件。
* [**StorPortEtwChannelEvent2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportetwevent2)、 [**StorPortEtwChannelEvent4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportetwevent4)和[**StorPortEtwChannelEvent8**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportetwevent8)允许微型端口将 ETW 事件发布到存储跟踪通道（Windows 10 1809 版及更高版本）。
* [**StorPortLogSystemEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportlogsystemevent)允许微型端口创建事件日志条目（Windows 7 和更高版本）。

Storport 在 "**Microsoft Windows-存储-Storport**" 提供程序名称下记录事件。 错误记录在**操作**通道中，调试/分析记录在**诊断**（**分析**和**调试**）中。 使用*事件查看器*应用程序时，必须首先启用**诊断**通道以查看它（若要启用，请单击 "*查看-> 显示分析和调试日志*"）。

 上述函数作为 Storport 扩展函数实现，可供使用现有扩展函数接口的微型端口驱动程序使用。 使用扩展函数接口可避免直接动态链接引用新函数。 通过避免直接引用，使用新函数的小型端口驱动程序会在不支持函数的操作系统上正常加载，并在不支持时返回 STOR_STATUS_NOT_IMPLEMENTED 的函数。 通过这种方式，供应商可以创建单个小型端口驱动程序，该驱动程序在多个操作系统版本上运行，并利用支持的新事件日志记录功能。

**注意：** 在 Windows 7 之前的 Storport 版本中，Storport 的系统事件日志接口（ [**StorPortLogError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportlogerror)）为微型端口驱动程序提供了内核系统事件日志工具的一小部分功能的访问权限，这将影响微型端口的有用性事件日志条目。

有关 Windows 事件的常规信息，请参阅[Windows 事件](https://docs.microsoft.com/windows/desktop/Events/windows-events)。
