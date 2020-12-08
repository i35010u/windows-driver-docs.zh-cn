---
title: NT 内核记录器跟踪会话
description: NT 内核记录器跟踪会话
keywords:
- 跟踪会话 WDK，NT 内核记录器
- NT 内核记录器跟踪会话 WDK
- Windows 内核跟踪提供程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ac03f0ba48c29270c8baaf840d6bca37e9e098a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806431"
---
# <a name="nt-kernel-logger-trace-session"></a>NT 内核记录器跟踪会话


NT 内核记录器跟踪会话生成 Windows 内核事件的跟踪。 它是内置于 Windows 中的保留跟踪会话。 您可以单独运行此跟踪会话，或在跟踪驱动程序时运行该会话，以便在驱动程序运行时显示 Windows 的操作。 [跟踪提供](trace-provider.md)程序（如内核模式驱动程序或用户模式应用程序）无法直接登录到此跟踪会话。

此跟踪会话使用保留的会话名称 "NT 内核记录器"，提供程序 GUID 由常量 **SystemTraceControlGuid** 表示。

若要创建 NT 内核记录器会话，请使用 [Tracelog](tracelog.md) 或 [TraceView](traceview.md)。

在 NT 内核记录器跟踪会话过程中跟踪的事件类型由事件 **member** \_ 跟踪属性结构的 EnableFlags 成员的值控制 \_ 。 此结构在 Microsoft Windows SDK 文档中进行了介绍。

默认情况下，当 Tracelog 启动 NT 内核记录器会话时，它将启用对进程、线程、物理磁盘 i/o 和 TCP/IP 事件的跟踪。 但是，可以通过以下方式启用或禁用对特定事件的跟踪：

-   使用 Tracelog 命令行参数。 有关详细信息，请参阅 [**Tracelog 命令语法**](tracelog-command-syntax.md)。

-   通过在 [TraceView](traceview.md) GUI 中设置复选框。

NT 内核记录器提供程序无法记录到其他跟踪会话，其他 [跟踪提供程序](trace-provider.md) 无法记录到 NT 内核记录器跟踪会话。 启动 NT 内核记录器跟踪会话时，不能使用 **-guid** 参数，并且不能在标准跟踪会话的 **guid** 参数中使用 NT 内核记录器跟踪会话的 guid。

若要从 "NT 内核记录器" 跟踪会话设置跟踪消息的格式，请将 Tracefmt 与 tmf 文件一起使用。 此文件包含在 WDK 中。

若要在系统启动期间跟踪内核事件，请将在系统启动期间跟踪的全局记录器跟踪会话转换为 NT 内核记录器跟踪会话。 有关信息，请参阅 [启动时全局记录器会话](boot-time-global-logger-session.md)

 

 





