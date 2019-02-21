---
title: NT 内核记录器跟踪会话
description: NT 内核记录器跟踪会话
ms.assetid: d805ae15-8946-4bb6-83b6-d5d31aacd456
keywords:
- 跟踪会话 WDK，NT 内核记录器
- NT 内核记录器跟踪会话 WDK
- Windows 内核跟踪提供程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8a03d693785cf574d5b11af39ab1ea9746f676b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555093"
---
# <a name="nt-kernel-logger-trace-session"></a>NT 内核记录器跟踪会话


NT 内核记录器跟踪会话生成 Windows 内核事件的跟踪。 它是内置于 Windows 的保留的跟踪会话。 可以单独运行此跟踪会话，或运行时跟踪驱动程序以运行该驱动程序时显示的 Windows 的操作。 [跟踪提供程序](trace-provider.md)，如内核模式驱动程序或用户模式应用程序，不能直接访问此跟踪会话日志。

此跟踪会话使用保留的会话名称，"NT 内核记录器"和提供程序 GUID 表示由常数**SystemTraceControlGuid**。

若要创建 NT 内核记录器会话，请使用[Tracelog](tracelog.md)或[TraceView](traceview.md)。

由 EnableFlags 的值控制在 NT 内核记录器跟踪会话期间进行跟踪的事件的类型**成员**的事件\_跟踪\_属性结构。 此结构是 Microsoft Windows SDK 文档中所述。

默认情况下，当 Tracelog 启动的 NT 内核记录器会话中，这样的进程、 线程、 物理磁盘 I/O、 跟踪和 TCP/IP 事件。 但是，可以启用或禁用特定事件的跟踪中的以下方法：

-   通过使用跟踪日志命令行参数。 有关详细信息，请参阅[ **Tracelog 命令语法**](tracelog-command-syntax.md)。

-   通过设置中的复选框[TraceView](traceview.md) GUI。

NT 内核记录器提供程序无法记录到其他跟踪会话和其他[跟踪提供程序](trace-provider.md)无法记录到 NT 内核记录器跟踪会话。 不能使用**guid**参数时启动的 NT 内核记录器跟踪会话，并且您不能使用 NT 内核记录器跟踪会话中的 GUID **guid**标准跟踪会话的参数。

要设置从 NT 内核记录器跟踪会话的跟踪消息的格式，请使用带有 system.tmf 文件 Tracefmt。 此文件包括在 WDK 中。

若要在系统启动期间跟踪内核事件，请将全局记录器跟踪会话，它跟踪在系统启动期间，转换为 NT 内核记录器跟踪会话。 有关信息，请参阅[启动时全局记录器会话](boot-time-global-logger-session.md)

 

 





