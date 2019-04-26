---
title: Windows 硬件错误体系结构的组件
description: Windows 硬件错误体系结构的组件
ms.assetid: d038f2ce-7012-4b8d-bf2b-a722548a32ca
keywords:
- Windows 硬件错误体系结构 WDK 组件
- WHEA WDK 组件
- 硬件错误 WDK WHEA，组件
- 错误 WDK WHEA，组件
- 组件 WDK WHEA
- 低级别的硬件错误处理程序 WDK WHEA
- LLHEHs WDK WHEA
- 特定于平台的硬件错误驱动程序 WDK WHEA
- PSHED WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f121486c0b7b207e865f0ab9657a1a0c6cc2f90
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327384"
---
# <a name="components-of-the-windows-hardware-error-architecture"></a>Windows 硬件错误体系结构的组件


下图显示了 Windows 硬件错误体系结构 (WHEA) 的主要组件。

![说明更换器驱动程序、 用户模式应用程序和服务、 大容量存储和端口驱动程序和换带机设备之间的关系的关系图](images/wheaarch.gif)

为每个硬件[错误源](hardware-errors-and-error-sources.md)是否发现的操作系统，具有对应*低级别的硬件错误处理程序*(LLHEH)。 LLHEH 是运行以响应的硬件错误条件的第一个操作系统代码。 LLHEH 可以中断处理程序、 异常处理程序、 一个轮询例程或由系统固件调用的回调例程。 在最合适的软件模块中实现每个 LLHEH： 对于 I/O 总线，它们存在于其各自的总线驱动程序;对于平台陷阱处理程序，它们存在于操作系统内核或硬件抽象层 (HAL)。

每个 LLHEH 执行以下任务：

-   确认硬件错误。

-   捕获与硬件错误相关的可用错误信息。

-   向操作系统报告的硬件错误条件。

通常情况下，LLHEHs 直接与硬件和固件检索硬件错误的信息进行交互。 LLHEHs 编译所有成硬件错误数据包与硬件错误相关的信息。 在固件最初处理硬件错误的情况下，相应 LLHEH 与要检索的错误数据包的固件进行交互。 所有 LLHEHs 向 Windows 操作系统内核中都报告硬件错误，通过将硬件错误数据包数据传递到常见的错误报告函数。

LLHEHs 和 Windows 内核可利用所提供的服务*特定于平台的硬件错误驱动程序*(PSHED) 来收集特定于平台的错误的信息。 PSHED 提供硬件错误报告的基础平台功能通过隐藏从操作系统平台的错误处理机制的详细信息，并公开 Windows 操作系统的一致界面的抽象。 对于涉及到硬件错误处理资源的系统固件接口的平台，PSHED 处理与固件进行交互。 这样，若要访问的错误状态的核心 Windows 组件注册被视为是同时还提供一种机制，通过该体系结构更丰富，可获得特定于平台的硬件错误的更多详细的信息。

对于每个处理器体系结构 (x 86、 x64 和 Itanium） 中，Microsoft 提供了实现核心错误处理行为，则为该体系结构常见 PSHED。 平台供应商可以通过提供 PSHED 插件，充分利用特定于平台的功能补充默认 PSHED 功能。 PSHED 插件是实现一个回调接口，由 PSHED 调用的专用的 Windows 设备驱动程序。 PSHED 插件旨在补充或替代由 Microsoft 提供 PSHED 的默认行为。

PSHED 插件旨在由平台供应商为硬件平台的硬件错误报告和恢复功能的软件接口实现。 PSHED 插件可与平台固件使用任何专用接口，或由平台供应商定义的机制。 这样，平台供应商联系以继续使用现有的固件硬件错误处理。 时间，Microsoft 需要更多的硬件错误报告和恢复功能将进行标准化。 因此 PSHED 插件的常规错误处理和报告需求将导致降低以便 PSHED 插件将仅需要支持提供附加价值超出标准硬件错误处理的特定于供应商的功能功能。

有关如何实现 PSHED 插件的详细信息，请参阅[特定于平台的硬件错误驱动程序插件](platform-specific-hardware-error-driver-plug-ins2.md)。

后通过 LLHEH 的硬件错误条件的通知，Windows 会创建[错误记录](error-records.md)以标准化格式描述硬件错误条件。 Windows 然后调入 PSHED，以便它可以将任何额外的硬件错误信息添加到要更好地描述硬件错误条件的错误记录。 如果 PSHED 插件已安装并且正在注册参与错误信息检索，PSHED 将反过来调入 PSHED 插件，以便它可以进一步扩充错误记录中的信息。 Windows 已编译的所有错误记录到硬件错误信息后，它在系统事件日志中记录错误消息，并通过引发事件跟踪 Windows (ETW) 事件来通知用户模式应用程序。

某些硬件错误情况下，操作系统将强制重新启动系统后，若要从错误中恢复。 在这些情况下，Windows 不在系统事件日志中记录错误信息或通知之前的用户模式应用程序后重新启动系统。 因此，操作系统前必须保存错误记录到某种形式的非易失性存储在系统重新启动。 PSHED 提供一个接口，通过该操作系统可以存储和检索错误记录，以便系统重新启动期间保留的错误信息。 如果 PSHED 插件安装，并且将注册为参与错误记录持久性，插件 PSHED 可以提供用于存储和检索错误记录的特定于平台的实现。 重新启动系统时，操作系统中检索已保存的错误记录，以便它可以正确记录在系统事件日志和用户模式应用程序可以收到通知。

WHEA 如何处理硬件错误的详细信息，请参阅[错误处理](error-processing.md)。

Windows 还提供了硬件错误管理 API，以便用户模式错误管理应用程序可以设置和检索硬件错误源信息、 配置错误处理的特定错误源，以及将硬件错误注入到硬件出于测试目的的平台。

有关如何实现 WHEA 管理应用程序的详细信息，请参阅[WHEA 管理应用程序](whea-management-applications.md)。

 

 




