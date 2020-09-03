---
title: 关于内核模式性能计数器
description: 关于内核模式性能计数器
ms.assetid: 57655e65-6db4-487d-8831-282e8d30d84e
ms.date: 08/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1e49bc431b34f79a831f04696be2ceb4a77d4c98
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89385065"
---
# <a name="about-kernel-mode-performance-counters"></a>关于内核模式性能计数器

性能计数器是组件发布的值，以允许系统管理员和开发人员了解组件的状态。 例如，网络组件可能会发布通过网络连接发送的数据包数。

Windows 性能计数器系统允许各种不同的组件通过一致且可发现的接口发布性能计数器。 Windows 性能计数器发布服务器通过 GUI 工具 (（例如 perfmon) 、命令行工具 (如 typeperf) ）和 Api (（例如 PDH 和 WMI) ）使用。 有关详细信息，请参阅 [性能计时器](/windows/win32/perfctrs/performance-counters-portal)。 发布性能计数器的组件称为性能计数器提供程序。

可以通过三种方式发布性能计数器值。

1. 用户模式组件 (例如，服务) 可以通过 [PerfLib api](/windows/win32/perfctrs/providing-counter-data-using-version-2-0)发布计数器。
2. 内核模式组件 (例如，驱动程序) 可以通过 [PCW api](using-kernel-mode-performance-counters.md)发布计数器。
3. 进程内 [性能扩展 DLL](/windows/win32/perfctrs/providing-counter-data-using-a-performance-dll) 可执行自定义集合。 请注意，进程内性能扩展 Dll 已弃用，由于性能和可靠性问题，新组件 **不应使用** 它们。

Windows (PCW 的性能计数器) 跟踪内核模式组件提供的 countersets。 它将使用者数据收集请求路由到相应的内核模式组件，并将请求的数据返回给用户模式使用者。

## <a name="related-topics"></a>相关主题

[使用内核模式性能计数器](using-kernel-mode-performance-counters.md)

[性能计数器门户](/windows/win32/perfctrs/performance-counters-portal)