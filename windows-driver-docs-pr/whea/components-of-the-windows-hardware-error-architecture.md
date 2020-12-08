---
title: Windows 硬件错误体系结构的组件
description: Windows 硬件错误体系结构的组件
keywords:
- Windows 硬件错误体系结构 WDK，组件
- WHEA WDK，组件
- 硬件错误 WDK WHEA，组件
- 错误 WDK WHEA，组件
- 组件 WDK WHEA
- 低级别硬件错误处理程序 WDK WHEA
- LLHEHs WDK WHEA
- 平台特定硬件错误驱动程序 WDK WHEA
- PSHED WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ab4ec8d54f515fd9034f33749039631156a2836
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822697"
---
# <a name="components-of-the-windows-hardware-error-architecture"></a>Windows 硬件错误体系结构的组件


下图显示了 (WHEA) 的 Windows 硬件错误体系结构的主要组件。

![说明更换器驱动程序、用户模式应用程序和服务、大容量存储和端口驱动程序以及更换器设备之间的关系的关系图](images/wheaarch.gif)

对于操作系统发现的每个硬件 [错误源](hardware-errors-and-error-sources.md) ，都有一个对应的 *低级别硬件错误处理程序* (LLHEH) 。 LLHEH 是为了响应硬件错误情况而运行的第一个操作系统代码。 LLHEH 可以是中断处理程序、异常处理程序、轮询例程或系统固件调用的回调例程。 每个 LLHEH 在最适当的软件模块中实现：对于 i/o 总线，它们存在于各自的总线驱动程序中;对于平台陷阱处理程序，它们存在于操作系统内核或硬件抽象层 (HAL) 。

每个 LLHEH 执行以下任务：

-   确认硬件错误。

-   捕获与硬件错误相关的可用错误信息。

-   向操作系统报告硬件错误条件。

通常，LLHEHs 会直接与硬件和固件交互，以检索硬件错误信息。 LLHEHs 将与硬件错误相关的所有信息编译为硬件错误数据包。 在固件最初处理硬件错误的情况下，相应的 LLHEH 与固件交互以检索错误数据包。 所有 LLHEHs 通过将硬件错误数据包数据传递给常见错误报告功能，将硬件错误报告给 Windows 操作系统内核。

LLHEHs 和 Windows 内核都) *平台特定硬件错误驱动程序* 的服务上进行绘制， (PSHED 收集平台特定的错误信息。 PSHED 通过从操作系统隐藏平台错误处理机制的详细信息，并向 Windows 操作系统公开一致的接口，来提供底层平台硬件错误报告功能的抽象。 在涉及系统固件接口到硬件错误处理资源的平台上，PSHED 处理与固件的交互。 这允许核心 Windows 组件仅访问被视为体系结构的错误状态寄存器，同时还提供一种机制，通过该机制可获取更丰富更详细的特定于平台的硬件错误信息。

对于每个处理器体系结构 (x86、x64 和 Itanium) ，Microsoft 提供了一个 PSHED 来实现此体系结构所共有的核心错误处理行为。 平台供应商可以通过提供利用特定于平台的功能的 PSHED 插件来补充默认的 PSHED 功能。 PSHED 插件是一种特殊用途的 Windows 设备驱动程序，可实现 PSHED 调用的回调接口。 PSHED 插件的用途是增加或覆盖 Microsoft 提供的 PSHED 的默认行为。

PSHED 插件旨在由平台供应商实现为硬件平台硬件错误报告和恢复功能的软件接口。 通过使用平台供应商定义的任何专用接口或机制，PSHED 插件可与平台固件交互。 这允许平台供应商继续使用现有固件进行硬件错误处理。 在此期间，Microsoft 期望将更多的硬件错误报告和恢复功能标准化。 因此，需要对 PSHED 插件进行常规错误处理和报告将会降低，这是因为仅支持供应商特定的功能，这些功能不仅提供标准硬件错误处理功能，还提供额外价值。

有关如何实现 PSHED 插件的详细信息，请参阅 [特定于平台的硬件错误驱动程序插件](platform-specific-hardware-error-driver-plug-ins2.md)。

当出现硬件错误情况 LLHEH 的通知时，Windows 会以标准化格式创建一个描述硬件错误情况的 [错误记录](error-records.md) 。 然后，Windows 调入 PSHED，以便可以将任何其他硬件错误信息添加到错误记录，以便更好地描述硬件错误情况。 如果安装了 PSHED 插件并注册了以参与错误信息检索，则 PSHED 将转到 PSHED 插件，以便进一步增加错误记录中的信息。 在 Windows 将所有硬件错误信息编译成错误记录后，它会将错误信息记录到系统事件日志中，并通过引发 Windows (ETW) 事件的事件跟踪来通知用户模式应用程序。

在某些硬件错误情况下，系统会强制重新启动系统以从错误中恢复。 在这些情况下，Windows 不会将错误信息记录在系统事件日志中，也不会通知用户模式应用程序，直到系统重新启动。 因此，在重新启动系统之前，操作系统必须将错误记录保存为某种形式的非易失性存储。 PSHED 提供了一个接口，操作系统可通过该接口存储和检索错误记录，以便在系统重新启动期间保留错误消息。 如果安装了 PSHED 插件并注册了以参与错误记录持久性，则 PSHED 插件可以为存储和检索错误记录提供特定于平台的实现。 重新启动系统时，操作系统将检索保存的错误记录，以便能够在系统事件日志中正确地记录该记录，并通知用户模式应用程序。

有关 WHEA 如何处理硬件错误的详细信息，请参阅 [错误处理](error-processing.md)。

Windows 还提供了硬件错误管理 API，使用户模式错误管理应用程序可以设置和检索硬件错误源信息，为特定错误源配置错误处理，并将硬件错误注入硬件平台进行测试。

有关如何实现 WHEA 管理应用程序的详细信息，请参阅 [WHEA 管理应用程序](whea-management-applications.md)。

 

 




