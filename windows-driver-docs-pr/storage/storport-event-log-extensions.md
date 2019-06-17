---
title: Storport 事件日志扩展
description: Storport 事件日志扩展
ms.assetid: 03b0bdef-cefa-4ad8-b9bf-a5f6b5f64cc6
ms.date: 06/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: f76a6a314679a3bd06f1fb41218b9894f669104f
ms.sourcegitcommit: e8b8c40d00a452793582f2729207b7d51bd89952
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67133889"
---
# <a name="storport-event-log-extensions"></a>Storport 事件日志扩展

许多其他类型的驱动程序，如 Storport 微型端口驱动程序必须在系统事件日志，以保留附加的存储设备的条件的通知的管理员创建项。 通常是以与设备相关的故障响应这些事件日志条目。 此外可以记录事件的遥测数据、 调试和优化。

Windows 内核本身提供灵活的接口，用于创建事件日志条目，尽管 Storport 微型端口模型不允许微型端口驱动程序直接访问该接口。 相反，Storport 提供内核的系统事件日志工具，周围的包装，微型端口驱动程序使用的包装器来创建事件日志条目。

具体而言，Storport 提供了以下事件日志例程：

* [**StorPortLogTelemetryEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportlogtelemetryex)允许微型端口 tracelogging 测量的日志或遥测事件的微型端口自定义数据 (Windows 10 1903年和更高版本)。
* [**StorPortEtwChannelEvent2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportetwevent2)， [ **StorPortEtwChannelEvent4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportetwevent4)，以及[ **StorPortEtwChannelEvent8** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportetwevent8)允许微型端口将 ETW 事件发布到存储跟踪通道 (Windows 10 1809年和更高版本)。
* [**StorPortLogSystemEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportlogsystemevent)允许微型端口创建一个事件日志条目 (Windows 7 和更高版本)。

Storport 记录下的事件"**Microsoft Windows 存储 Storport**"提供程序名称。 在中记录错误**Operational**通道，而调试/分析中将记录**诊断**(**分析**并**调试**)。 使用时*事件查看器*应用程序，必须首先启用**诊断**通道，以查看它 (若要启用，请单击*视图-> 显示分析和调试日志*)。

 上述函数作为 Storport 扩展函数实现，并可供使用的现有扩展的函数接口的微型端口驱动程序。 使用扩展的函数接口可避免对新函数的直接动态链接引用。 通过避免该直接引用，使用新的函数的微型端口驱动程序正确加载不支持的函数，函数返回 STOR_STATUS_NOT_IMPLEMENTED 时不支持的操作系统上。 这样一来，供应商可以创建在多个 OS 版本运行单个的微型端口驱动程序充分利用新的事件日志记录函数支持的。

**注意：** 在版本的 Windows 7，Storport 的系统事件日志界面之前, Storport [ **StorPortLogError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportlogerror)，提供给内核的系统事件的功能的一小部分的微型端口驱动程序访问日志工具，这会影响微型端口事件日志条目的实用性。

有关 Windows 事件的常规信息，请参阅[Windows 事件](https://docs.microsoft.com/windows/desktop/Events/windows-events)。
